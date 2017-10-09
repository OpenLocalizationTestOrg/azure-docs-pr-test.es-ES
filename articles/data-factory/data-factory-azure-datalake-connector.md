---
title: "aaaCopy tooand de datos de almacén de Azure Data Lake | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocopy tooand de datos de almacén de Data Lake mediante el uso de Data Factory de Azure"
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
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="36292-103">Copiar datos tooand de almacén de Data Lake con factoría de datos</span><span class="sxs-lookup"><span data-stu-id="36292-103">Copy data tooand from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="36292-104">Este artículo se explica cómo toouse actividad de copia de Data Factory de Azure toomove datos tooand de almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="36292-104">This article explains how toouse Copy Activity in Azure Data Factory toomove data tooand from Azure Data Lake Store.</span></span> <span data-ttu-id="36292-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, información general sobre el movimiento de datos con la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="36292-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="36292-106">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="36292-106">Supported scenarios</span></span>
<span data-ttu-id="36292-107">Puede copiar datos **de almacén de Azure Data Lake** toohello siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="36292-107">You can copy data **from Azure Data Lake Store** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="36292-108">Puede copiar los datos de hello siguientes almacenes de datos **tooAzure almacén de Data Lake**:</span><span class="sxs-lookup"><span data-stu-id="36292-108">You can copy data from hello following data stores **tooAzure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="36292-109">Cree una cuenta de Data Lake Store antes de crear una canalización con la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="36292-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="36292-110">Para más información, consulte [Introducción a Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="36292-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="36292-111">Tipos de autenticación que se admiten</span><span class="sxs-lookup"><span data-stu-id="36292-111">Supported authentication types</span></span>
<span data-ttu-id="36292-112">Conector de almacén de Data Lake Hello es compatible con estos tipos de autenticación:</span><span class="sxs-lookup"><span data-stu-id="36292-112">hello Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="36292-113">Autenticación de entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="36292-113">Service principal authentication</span></span>
* <span data-ttu-id="36292-114">Autenticación de credenciales de usuario (OAuth)</span><span class="sxs-lookup"><span data-stu-id="36292-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="36292-115">Se recomienda que use la autenticación de la entidad de servicio, en especial para una copia de datos programada.</span><span class="sxs-lookup"><span data-stu-id="36292-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="36292-116">Con la autenticación se credenciales de usuario puede darse la situación de que expiren los tokens.</span><span class="sxs-lookup"><span data-stu-id="36292-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="36292-117">Para obtener detalles de configuración, vea hello [vinculado propiedades del servicio](#linked-service-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="36292-117">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="36292-118">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="36292-118">Get started</span></span>
<span data-ttu-id="36292-119">Puede crear una canalización con actividad de copia que mueva los datos hacia Azure Data Lake Store y desde este servicio mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="36292-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="36292-120">toocreate de manera más fácil de Hello datos toocopy canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="36292-120">hello easiest way toocreate a pipeline toocopy data is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="36292-121">Para obtener un tutorial sobre cómo crear una canalización mediante Hola Asistente para copiar, consulte [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="36292-121">For a tutorial on creating a pipeline by using hello Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="36292-122">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="36292-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="36292-123">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="36292-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="36292-124">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="36292-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="36292-125">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="36292-125">Create a **data factory**.</span></span> <span data-ttu-id="36292-126">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="36292-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="36292-127">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="36292-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="36292-128">Por ejemplo, si va a copiar datos desde un tooan de almacenamiento de blobs de Azure almacén de Data Lake de Azure, cree dos toolink servicios vinculados su cuenta de almacenamiento de Azure y la factoría de datos de Azure Data Lake almacén tooyour.</span><span class="sxs-lookup"><span data-stu-id="36292-128">For example, if you are copying data from an Azure blob storage tooan Azure Data Lake Store, you create two linked services toolink your Azure storage account and Azure Data Lake store tooyour data factory.</span></span> <span data-ttu-id="36292-129">Para las propiedades de servicio vinculado que son específico tooAzure almacén de Data Lake, consulte [vinculado propiedades del servicio](#linked-service-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="36292-129">For linked service properties that are specific tooAzure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="36292-130">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="36292-131">En el ejemplo de Hola mencionado en el último paso de hello, se crea un contenedor de blobs de hello toospecify de conjunto de datos y la carpeta que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-131">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="36292-132">Y crear otra conjunto de datos toospecify Hola carpeta y la ruta en el almacén de Data Lake de Hola que contiene datos de hello copiados desde el almacenamiento de blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-132">And, you create another dataset toospecify hello folder and file path in hello Data Lake store that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="36292-133">Para las propiedades del conjunto de datos que son específico tooAzure almacén de Data Lake, consulte [propiedades de conjunto de datos](#dataset-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="36292-133">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="36292-134">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="36292-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="36292-135">En el ejemplo de Hola que se ha mencionado anteriormente, use BlobSource como un origen y AzureDataLakeStoreSink como un receptor para la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-135">In hello example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for hello copy activity.</span></span> <span data-ttu-id="36292-136">De forma similar, si va a copiar desde el almacén de Azure Data Lake tooAzure almacenamiento de blobs, usar AzureDataLakeStoreSource y BlobSink de actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-136">Similarly, if you are copying from Azure Data Lake Store tooAzure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in hello copy activity.</span></span> <span data-ttu-id="36292-137">Para copiar propiedades de actividad que son específico tooAzure almacén de Data Lake, consulte [copiar propiedades de la actividad](#copy-activity-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="36292-137">For copy activity properties that are specific tooAzure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="36292-138">Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="36292-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="36292-139">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="36292-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="36292-140">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="36292-141">Para obtener ejemplos con definiciones de JSON para entidades de factoría de datos que son utilizados toocopy datos hacia y desde un almacén de Data Lake de Azure, vea [ejemplos JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="36292-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="36292-142">Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizado toodefine factoría de datos de entidades específico tooData Lake almacén.</span><span class="sxs-lookup"><span data-stu-id="36292-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooData Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="36292-143">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="36292-143">Linked service properties</span></span>
<span data-ttu-id="36292-144">Un servicio vinculado vincula una factoría de datos de tooa de almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="36292-144">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="36292-145">Crear un servicio vinculado de tipo **AzureDataLakeStore** toolink su factoría de datos de almacén de Data Lake datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="36292-145">You create a linked service of type **AzureDataLakeStore** toolink your Data Lake Store data tooyour data factory.</span></span> <span data-ttu-id="36292-146">Hello en la tabla siguiente describe los servicios de tooData Lake almacén vinculado específicos de elementos JSON.</span><span class="sxs-lookup"><span data-stu-id="36292-146">hello following table describes JSON elements specific tooData Lake Store linked services.</span></span> <span data-ttu-id="36292-147">Puede elegir entre la autenticación de la entidad de servicio y la autenticación de credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="36292-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="36292-148">Propiedad</span><span class="sxs-lookup"><span data-stu-id="36292-148">Property</span></span> | <span data-ttu-id="36292-149">Descripción</span><span class="sxs-lookup"><span data-stu-id="36292-149">Description</span></span> | <span data-ttu-id="36292-150">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="36292-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="36292-151">**type**</span><span class="sxs-lookup"><span data-stu-id="36292-151">**type**</span></span> | <span data-ttu-id="36292-152">se debe establecer propiedad de tipo Hello demasiado**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="36292-152">hello type property must be set too**AzureDataLakeStore**.</span></span> | <span data-ttu-id="36292-153">Sí</span><span class="sxs-lookup"><span data-stu-id="36292-153">Yes</span></span> |
| <span data-ttu-id="36292-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="36292-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="36292-155">Información acerca de la cuenta de almacén de Azure Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-155">Information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="36292-156">Esta información toma una de hello siguientes formatos: `https://[accountname].azuredatalakestore.net/webhdfs/v1` o `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="36292-156">This information takes one of hello following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="36292-157">Sí</span><span class="sxs-lookup"><span data-stu-id="36292-157">Yes</span></span> |
| <span data-ttu-id="36292-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="36292-158">**subscriptionId**</span></span> | <span data-ttu-id="36292-159">Hola de toowhich de Id. de suscripción de Azure cuenta de almacén de Data Lake pertenece.</span><span class="sxs-lookup"><span data-stu-id="36292-159">Azure subscription ID toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="36292-160">Necesario para el receptor</span><span class="sxs-lookup"><span data-stu-id="36292-160">Required for sink</span></span> |
| <span data-ttu-id="36292-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="36292-161">**resourceGroupName**</span></span> | <span data-ttu-id="36292-162">Hola de toowhich de nombre de grupo de recursos de Azure cuenta de almacén de Data Lake pertenece.</span><span class="sxs-lookup"><span data-stu-id="36292-162">Azure resource group name toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="36292-163">Necesario para el receptor</span><span class="sxs-lookup"><span data-stu-id="36292-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="36292-164">Autenticación de la entidad de servicio (recomendada)</span><span class="sxs-lookup"><span data-stu-id="36292-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="36292-165">toouse autenticación principal del servicio, registrar una entidad de la aplicación en Azure Active Directory (Azure AD) y conceda a Hola acceso tooData Lake almacén.</span><span class="sxs-lookup"><span data-stu-id="36292-165">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="36292-166">Consulte [Autenticación entre servicios](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) para ver los pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="36292-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="36292-167">Tome nota de hello después de valores, que se utiliza toodefine Hola servicio vinculado:</span><span class="sxs-lookup"><span data-stu-id="36292-167">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="36292-168">Identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="36292-168">Application ID</span></span>
* <span data-ttu-id="36292-169">Clave de la aplicación</span><span class="sxs-lookup"><span data-stu-id="36292-169">Application key</span></span> 
* <span data-ttu-id="36292-170">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="36292-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36292-171">Si usas las canalizaciones de datos de hello Asistente para copiar tooauthor, asegúrese de que concedan entidad de servicio de hello al menos un **lector** rol en el control de acceso (administración de identidades y acceso) para la cuenta de almacén de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-171">If you are using hello Copy Wizard tooauthor data pipelines, make sure that you grant hello service principal at least a **Reader** role in access control (identity and access management) for hello Data Lake Store account.</span></span> <span data-ttu-id="36292-172">Además, al menos a conceder entidad de servicio de Hola **lectura + Execute** raíz de almacén de Data Lake tooyour de permiso ("/") y sus elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="36292-172">Also, grant hello service principal at least **Read + Execute** permission tooyour Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="36292-173">En caso contrario, puede aparecer el mensaje de Hola "hello las credenciales proporcionaron no son válidos".</span><span class="sxs-lookup"><span data-stu-id="36292-173">Otherwise you might see hello message "hello credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="36292-174">Después de crear o actualizar a una entidad de servicio en Azure AD, puede tardar unos minutos para hello cambios tootake efecto.</span><span class="sxs-lookup"><span data-stu-id="36292-174">After you create or update a service principal in Azure AD, it can take a few minutes for hello changes tootake effect.</span></span> <span data-ttu-id="36292-175">Compruebe la entidad de servicio de Hola y configuraciones de lista (ACL) de control de acceso de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="36292-175">Check hello service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="36292-176">Si todavía aparece el mensaje de saludo "¡hello las credenciales proporcionaron no son válidos", espere unos instantes e inténtelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="36292-176">If you still see hello message "hello credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="36292-177">Utilizar autenticación de entidad de seguridad de servicio mediante la especificación de hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="36292-177">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="36292-178">Propiedad</span><span class="sxs-lookup"><span data-stu-id="36292-178">Property</span></span> | <span data-ttu-id="36292-179">Descripción</span><span class="sxs-lookup"><span data-stu-id="36292-179">Description</span></span> | <span data-ttu-id="36292-180">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="36292-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="36292-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="36292-181">**servicePrincipalId**</span></span> | <span data-ttu-id="36292-182">Especifique el identificador de cliente de. la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="36292-182">Specify hello application's client ID.</span></span> | <span data-ttu-id="36292-183">Sí</span><span class="sxs-lookup"><span data-stu-id="36292-183">Yes</span></span> |
| <span data-ttu-id="36292-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="36292-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="36292-185">Especifique la clave de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="36292-185">Specify hello application's key.</span></span> | <span data-ttu-id="36292-186">Sí</span><span class="sxs-lookup"><span data-stu-id="36292-186">Yes</span></span> |
| <span data-ttu-id="36292-187">**tenant**</span><span class="sxs-lookup"><span data-stu-id="36292-187">**tenant**</span></span> | <span data-ttu-id="36292-188">Especifique la información de inquilino de hello (inquilino o el nombre de identificador de dominio) en que se encuentra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="36292-188">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="36292-189">Puede recuperarlo mediante el desplazamiento del mouse de hello en la esquina superior derecha de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="36292-189">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="36292-190">Sí</span><span class="sxs-lookup"><span data-stu-id="36292-190">Yes</span></span> |

<span data-ttu-id="36292-191">**Ejemplo: autenticación de la entidad de servicio**</span><span class="sxs-lookup"><span data-stu-id="36292-191">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="36292-192">Autenticación de credenciales de usuario</span><span class="sxs-lookup"><span data-stu-id="36292-192">User credential authentication</span></span>
<span data-ttu-id="36292-193">Como alternativa, puede usar toocopy de autenticación de credenciales de usuario de o tooData Lake almacén mediante la especificación de hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="36292-193">Alternatively, you can use user credential authentication toocopy from or tooData Lake Store by specifying hello following properties:</span></span>

| <span data-ttu-id="36292-194">Propiedad</span><span class="sxs-lookup"><span data-stu-id="36292-194">Property</span></span> | <span data-ttu-id="36292-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="36292-195">Description</span></span> | <span data-ttu-id="36292-196">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="36292-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="36292-197">**authorization**</span><span class="sxs-lookup"><span data-stu-id="36292-197">**authorization**</span></span> | <span data-ttu-id="36292-198">Haga clic en hello **Authorize** botón Hola Editor de generador de datos y escriba sus credenciales que asigna la propiedad de hello autogenerado autorización URL toothis.</span><span class="sxs-lookup"><span data-stu-id="36292-198">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="36292-199">Sí</span><span class="sxs-lookup"><span data-stu-id="36292-199">Yes</span></span> |
| <span data-ttu-id="36292-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="36292-200">**sessionId**</span></span> | <span data-ttu-id="36292-201">Identificador de sesión de OAuth de sesión de autorización de OAuth de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-201">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="36292-202">Cada id. de sesión es único y solo se puede usar una vez.</span><span class="sxs-lookup"><span data-stu-id="36292-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="36292-203">Esta configuración se genera automáticamente cuando se usa Hola Editor de generador de datos.</span><span class="sxs-lookup"><span data-stu-id="36292-203">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="36292-204">Sí</span><span class="sxs-lookup"><span data-stu-id="36292-204">Yes</span></span> |

<span data-ttu-id="36292-205">**Ejemplo: autenticación de credenciales de usuario**</span><span class="sxs-lookup"><span data-stu-id="36292-205">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="36292-206">Expiración del token</span><span class="sxs-lookup"><span data-stu-id="36292-206">Token expiration</span></span>
<span data-ttu-id="36292-207">Hola código de autorización que genera mediante el uso de hello **Authorize** botón expira transcurrido un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="36292-207">hello authorization code that you generate by using hello **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="36292-208">Hola sigue mensaje significa que ese token de autenticación Hola expiró:</span><span class="sxs-lookup"><span data-stu-id="36292-208">hello following message means that hello authentication token has expired:</span></span>

<span data-ttu-id="36292-209">Error de operación de credencial: invalid_grant - AADSTS70002: error al validar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="36292-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="36292-210">AADSTS70008: Hola proporciona concesión de acceso expiró o se revocó.</span><span class="sxs-lookup"><span data-stu-id="36292-210">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="36292-211">Id. de seguimiento: d18629e8-af88-43c5-88e3-d8419eb1fca1 Id. de correlación: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Marca de tiempo: 2015-12-15 21:09:31Z.</span><span class="sxs-lookup"><span data-stu-id="36292-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="36292-212">Hello tabla siguiente muestran los tiempos de expiración de Hola de diferentes tipos de cuentas de usuario:</span><span class="sxs-lookup"><span data-stu-id="36292-212">hello following table shows hello expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="36292-213">Tipo de usuario</span><span class="sxs-lookup"><span data-stu-id="36292-213">User type</span></span> | <span data-ttu-id="36292-214">Expira después de</span><span class="sxs-lookup"><span data-stu-id="36292-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="36292-215">Cuentas de usuario *no* administradas por Azure Active Directory (por ejemplo, @hotmail.com o @live.com)</span><span class="sxs-lookup"><span data-stu-id="36292-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="36292-216">12 horas</span><span class="sxs-lookup"><span data-stu-id="36292-216">12 hours</span></span> |
| <span data-ttu-id="36292-217">Cuentas de usuario administradas por Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36292-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="36292-218">ejecutar 14 días después de último segmento de Hola</span><span class="sxs-lookup"><span data-stu-id="36292-218">14 days after hello last slice run</span></span> <br/><br/><span data-ttu-id="36292-219">90 días, si un segmento basado en un servicio vinculado basado en OAuth se ejecuta al menos una vez cada 14 días.</span><span class="sxs-lookup"><span data-stu-id="36292-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="36292-220">Si cambia la contraseña anterior a la hora de expiración del token de hello, símbolo (token) de hello caduca inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="36292-220">If you change your password before hello token expiration time, hello token expires immediately.</span></span> <span data-ttu-id="36292-221">Verá mensajes de bienvenida se ha mencionado anteriormente en esta sección.</span><span class="sxs-lookup"><span data-stu-id="36292-221">You will see hello message mentioned earlier in this section.</span></span>

<span data-ttu-id="36292-222">Puede autorizar la cuenta de hello mediante el uso de hello **Authorize** botón cuando caduca de token de Hola Hola tooredeploy servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="36292-222">You can reauthorize hello account by using hello **Authorize** button when hello token expires tooredeploy hello linked service.</span></span> <span data-ttu-id="36292-223">También pueden generar valores de hello **sessionId** y **autorización** Hola propiedades mediante programación mediante el uso de código siguiente:</span><span class="sxs-lookup"><span data-stu-id="36292-223">You can also generate values for hello **sessionId** and **authorization** properties programmatically by using hello following code:</span></span>


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
<span data-ttu-id="36292-224">Para obtener más información acerca de las clases de factoría de datos de hello usarse en el código de hello, vea hello [azuredatalakestorelinkedservice clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), y [ Clase AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) temas.</span><span class="sxs-lookup"><span data-stu-id="36292-224">For details about hello Data Factory classes used in hello code, see hello [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="36292-225">Agregar una referencia tooversion `2.9.10826.1824` de `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` para hello `WindowsFormsWebAuthenticationDialog` clase usada en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="36292-225">Add a reference tooversion `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for hello `WindowsFormsWebAuthenticationDialog` class used in hello code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="36292-226">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="36292-226">Dataset properties</span></span>
<span data-ttu-id="36292-227">un conjunto de datos toorepresent datos de entrada en un almacén de Data Lake toospecify, Establece hello **tipo** propiedad del conjunto de datos de hello demasiado**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="36292-227">toospecify a dataset toorepresent input data in a Data Lake Store, you set hello **type** property of hello dataset too**AzureDataLakeStore**.</span></span> <span data-ttu-id="36292-228">Conjunto hello **linkedServiceName** propiedad del nombre de toohello Hola conjunto de datos de almacén de Data Lake hello servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="36292-228">Set hello **linkedServiceName** property of hello dataset toohello name of hello Data Lake Store linked service.</span></span> <span data-ttu-id="36292-229">Para obtener una lista completa de las secciones JSON y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="36292-229">For a full list of JSON sections and properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="36292-230">Las secciones de un conjunto de datos de JSON, como **structure**, **availability** y **policy**, son similares para todos los tipos de datos (base de datos SQL de Azure, blob de Azure y tabla de Azure, por ejemplo).</span><span class="sxs-lookup"><span data-stu-id="36292-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="36292-231">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información como la ubicación y el formato de datos de hello en el almacén de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-231">hello **typeProperties** section is different for each type of dataset and provides information such as location and format of hello data in hello data store.</span></span> 

<span data-ttu-id="36292-232">Hola **typeProperties** sección para un conjunto de datos de tipo **AzureDataLakeStore** contiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="36292-232">hello **typeProperties** section for a dataset of type **AzureDataLakeStore** contains hello following properties:</span></span>

| <span data-ttu-id="36292-233">Propiedad</span><span class="sxs-lookup"><span data-stu-id="36292-233">Property</span></span> | <span data-ttu-id="36292-234">Descripción</span><span class="sxs-lookup"><span data-stu-id="36292-234">Description</span></span> | <span data-ttu-id="36292-235">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="36292-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="36292-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="36292-236">**folderPath**</span></span> |<span data-ttu-id="36292-237">Contenedor de toohello de ruta de acceso y la carpeta en el almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="36292-237">Path toohello container and folder in Data Lake Store.</span></span> |<span data-ttu-id="36292-238">Sí</span><span class="sxs-lookup"><span data-stu-id="36292-238">Yes</span></span> |
| <span data-ttu-id="36292-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="36292-239">**fileName**</span></span> |<span data-ttu-id="36292-240">Nombre del archivo de hello en el almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="36292-240">Name of hello file in Azure Data Lake Store.</span></span> <span data-ttu-id="36292-241">Hola **fileName** propiedad es opcional y distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="36292-241">hello **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="36292-242">Si especifica **fileName**, actividad de hello (incluida la copia) funciona en archivos específicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-242">If you specify **fileName**, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="36292-243">Cuando **fileName** no se especifica, copia incluye todos los archivos en **folderPath** en el conjunto de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-243">When **fileName** is not specified, Copy includes all files in **folderPath** in hello input dataset.</span></span><br/><br/><span data-ttu-id="36292-244">Cuando **fileName** no se especifica para un conjunto de datos de salida y **preserveHierarchy** no se especifica en el receptor de actividad, nombre de Hola de archivo hello generado está en formato de hello datos. _GUID_.txt'.</span><span class="sxs-lookup"><span data-stu-id="36292-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello format Data._Guid_.txt\`.</span></span> <span data-ttu-id="36292-245">Por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="36292-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="36292-246">No</span><span class="sxs-lookup"><span data-stu-id="36292-246">No</span></span> |
| <span data-ttu-id="36292-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="36292-247">**partitionedBy**</span></span> |<span data-ttu-id="36292-248">Hola **partitionedBy** propiedad es opcional.</span><span class="sxs-lookup"><span data-stu-id="36292-248">hello **partitionedBy** property is optional.</span></span> <span data-ttu-id="36292-249">Puede usarlo toospecify una ruta de acceso dinámico y el nombre de archivo de datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="36292-249">You can use it toospecify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="36292-250">Por ejemplo, se puede parametrizar **folderPath** por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="36292-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="36292-251">Para obtener más información y ejemplos, vea [Hola propiedad partitionedBy](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="36292-251">For details and examples, see [hello partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="36292-252">No</span><span class="sxs-lookup"><span data-stu-id="36292-252">No</span></span> |
| <span data-ttu-id="36292-253">**format**</span><span class="sxs-lookup"><span data-stu-id="36292-253">**format**</span></span> | <span data-ttu-id="36292-254">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, y  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="36292-254">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="36292-255">Conjunto hello **tipo** propiedad bajo **formato** tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="36292-255">Set hello **type** property under **format** tooone of these values.</span></span> <span data-ttu-id="36292-256">Para obtener más información, vea hello [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [el formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato ORC](data-factory-supported-file-and-compression-formats.md#orc-format), y [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) secciones de hello [compresión de archivos y formatos admitidos por factoría de datos de Azure](data-factory-supported-file-and-compression-formats.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="36292-256">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in hello [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="36292-257">Si desea que los archivos de toocopy "como-es" entre los almacenes basados en archivos (copia binaria), omitir hello `format` sección en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="36292-257">If you want toocopy files "as-is" between file-based stores (binary copy), skip hello `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="36292-258">No</span><span class="sxs-lookup"><span data-stu-id="36292-258">No</span></span> |
| <span data-ttu-id="36292-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="36292-259">**compression**</span></span> | <span data-ttu-id="36292-260">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-260">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="36292-261">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="36292-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="36292-262">Niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="36292-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="36292-263">Para más información, consulte el artículo sobre [Formatos de compresión de archivos admitidos por Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="36292-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="36292-264">No</span><span class="sxs-lookup"><span data-stu-id="36292-264">No</span></span> |

### <a name="hello-partitionedby-property"></a><span data-ttu-id="36292-265">propiedad de Hello partitionedBy</span><span class="sxs-lookup"><span data-stu-id="36292-265">hello partitionedBy property</span></span>
<span data-ttu-id="36292-266">Puede especificar dinámica **folderPath** y **fileName** propiedades para los datos de serie temporal con hello **partitionedBy** propiedad, funciones de factoría de datos y sistema variables.</span><span class="sxs-lookup"><span data-stu-id="36292-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with hello **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="36292-267">Para obtener más información, vea hello [factoría de datos de Azure: funciones y variables del sistema](data-factory-functions-variables.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="36292-267">For details, see hello [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="36292-268">En el siguiente ejemplo, el Hola `{Slice}` se reemplaza con el valor de Hola de variable del sistema Hola factoría de datos `SliceStart` en formato de hello especificado (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="36292-268">In hello following example, `{Slice}` is replaced with hello value of hello Data Factory system variable `SliceStart` in hello format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="36292-269">nombre de Hello `SliceStart` hace referencia toohello hora de inicio del segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-269">hello name `SliceStart` refers toohello start time of hello slice.</span></span> <span data-ttu-id="36292-270">Hola `folderPath` propiedad es diferente para cada segmento, como en `wikidatagateway/wikisampledataout/2014100103` o `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="36292-270">hello `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="36292-271">Hola siguiente ejemplo, año hello, mes, día y hora de `SliceStart` se extraen en variables independientes que usan hello `folderPath` y `fileName` propiedades:</span><span class="sxs-lookup"><span data-stu-id="36292-271">In hello following example, hello year, month, day, and time of `SliceStart` are extracted into separate variables that are used by hello `folderPath` and `fileName` properties:</span></span>
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
<span data-ttu-id="36292-272">Para obtener más detalles sobre los conjuntos de datos de series temporales, programación y segmentos, vea hello [conjuntos de datos de Data Factory de Azure](data-factory-create-datasets.md) y [programación de la factoría de datos y la ejecución](data-factory-scheduling-and-execution.md) artículos.</span><span class="sxs-lookup"><span data-stu-id="36292-272">For more details on time-series datasets, scheduling, and slices, see hello [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="36292-273">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="36292-273">Copy activity properties</span></span>
<span data-ttu-id="36292-274">Para obtener una lista completa de las secciones y las propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="36292-274">For a full list of sections and properties available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="36292-275">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="36292-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="36292-276">Hola propiedades disponibles en hello **typeProperties** sección de una actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="36292-276">hello properties available in hello **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="36292-277">Para una actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="36292-277">For a copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="36292-278">**AzureDataLakeStoreSource** admite Hola después propiedad Hola **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="36292-278">**AzureDataLakeStoreSource** supports hello following property in hello **typeProperties** section:</span></span>

| <span data-ttu-id="36292-279">Propiedad</span><span class="sxs-lookup"><span data-stu-id="36292-279">Property</span></span> | <span data-ttu-id="36292-280">Descripción</span><span class="sxs-lookup"><span data-stu-id="36292-280">Description</span></span> | <span data-ttu-id="36292-281">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="36292-281">Allowed values</span></span> | <span data-ttu-id="36292-282">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="36292-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36292-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="36292-283">**recursive**</span></span> |<span data-ttu-id="36292-284">Indica si los datos de Hola es de lectura de forma recursiva de las subcarpetas de Hola o solo de la carpeta especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-284">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="36292-285">True (valor predeterminado), False</span><span class="sxs-lookup"><span data-stu-id="36292-285">True (default value), False</span></span> |<span data-ttu-id="36292-286">No</span><span class="sxs-lookup"><span data-stu-id="36292-286">No</span></span> |


<span data-ttu-id="36292-287">**AzureDataLakeStoreSink** admite Hola propiedades Hola siguientes **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="36292-287">**AzureDataLakeStoreSink** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="36292-288">Propiedad</span><span class="sxs-lookup"><span data-stu-id="36292-288">Property</span></span> | <span data-ttu-id="36292-289">Descripción</span><span class="sxs-lookup"><span data-stu-id="36292-289">Description</span></span> | <span data-ttu-id="36292-290">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="36292-290">Allowed values</span></span> | <span data-ttu-id="36292-291">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="36292-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36292-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="36292-292">**copyBehavior**</span></span> |<span data-ttu-id="36292-293">Especifica el comportamiento de la copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-293">Specifies hello copy behavior.</span></span> |<span data-ttu-id="36292-294"><b>PreserveHierarchy</b>: conserva la jerarquía de archivos de hello en la carpeta de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-294"><b>PreserveHierarchy</b>: Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="36292-295">ruta de acceso relativa de Hola de carpeta de origen del archivo toosource es idéntico toohello ruta de acceso relativa de la carpeta de tootarget de archivo de destino.</span><span class="sxs-lookup"><span data-stu-id="36292-295">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="36292-296"><b>FlattenHierarchy</b>: todos los archivos de la carpeta de origen Hola se crean en el primer nivel de carpeta de destino de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-296"><b>FlattenHierarchy</b>: All files from hello source folder are created in hello first level of hello target folder.</span></span> <span data-ttu-id="36292-297">archivos de destino de Hola se crean con nombres generados automáticamente.</span><span class="sxs-lookup"><span data-stu-id="36292-297">hello target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="36292-298"><b>MergeFiles</b>: combina todos los archivos del archivo de tooone de carpeta de origen de hello.</span><span class="sxs-lookup"><span data-stu-id="36292-298"><b>MergeFiles</b>: Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="36292-299">Si hello nombre de archivo o blob no se especifica, nombre de archivo combinado de hello es nombre especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-299">If hello file or blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="36292-300">En caso contrario, el nombre del archivo de hello es generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="36292-300">Otherwise, hello file name is autogenerated.</span></span> |<span data-ttu-id="36292-301">No</span><span class="sxs-lookup"><span data-stu-id="36292-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="36292-302">Ejemplos de recursive y copyBehavior</span><span class="sxs-lookup"><span data-stu-id="36292-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="36292-303">Esta sección describe el comportamiento resultante de Hola de operación de copia de Hola para diferentes combinaciones de valores recursiva y copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="36292-303">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="36292-304">recursive</span><span class="sxs-lookup"><span data-stu-id="36292-304">recursive</span></span> | <span data-ttu-id="36292-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="36292-305">copyBehavior</span></span> | <span data-ttu-id="36292-306">Comportamiento resultante</span><span class="sxs-lookup"><span data-stu-id="36292-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36292-307">true</span><span class="sxs-lookup"><span data-stu-id="36292-307">true</span></span> |<span data-ttu-id="36292-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="36292-308">preserveHierarchy</span></span> |<span data-ttu-id="36292-309">Para una carpeta de origen carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="36292-309">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="36292-310">Folder1</span><span class="sxs-lookup"><span data-stu-id="36292-310">Folder1</span></span><br/><span data-ttu-id="36292-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="36292-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="36292-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="36292-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="36292-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="36292-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="36292-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="36292-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="36292-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="36292-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="36292-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="36292-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="36292-317">se crea la carpeta de destino de Hello carpeta1 con hello misma estructura como origen de Hola</span><span class="sxs-lookup"><span data-stu-id="36292-317">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="36292-318">Folder1</span><span class="sxs-lookup"><span data-stu-id="36292-318">Folder1</span></span><br/><span data-ttu-id="36292-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="36292-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="36292-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="36292-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="36292-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="36292-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="36292-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="36292-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="36292-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="36292-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="36292-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="36292-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="36292-325">true</span><span class="sxs-lookup"><span data-stu-id="36292-325">true</span></span> |<span data-ttu-id="36292-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="36292-326">flattenHierarchy</span></span> |<span data-ttu-id="36292-327">Para una carpeta de origen carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="36292-327">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="36292-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="36292-328">Folder1</span></span><br/><span data-ttu-id="36292-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="36292-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="36292-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="36292-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="36292-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="36292-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="36292-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="36292-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="36292-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="36292-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="36292-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="36292-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="36292-335">se crea el destino de Hola carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="36292-335">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="36292-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="36292-336">Folder1</span></span><br/><span data-ttu-id="36292-337">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="36292-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="36292-338">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2</span><span class="sxs-lookup"><span data-stu-id="36292-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="36292-339">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File3</span><span class="sxs-lookup"><span data-stu-id="36292-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="36292-340">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File4</span><span class="sxs-lookup"><span data-stu-id="36292-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="36292-341">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File5</span><span class="sxs-lookup"><span data-stu-id="36292-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="36292-342">true</span><span class="sxs-lookup"><span data-stu-id="36292-342">true</span></span> |<span data-ttu-id="36292-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="36292-343">mergeFiles</span></span> |<span data-ttu-id="36292-344">Para una carpeta de origen carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="36292-344">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="36292-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="36292-345">Folder1</span></span><br/><span data-ttu-id="36292-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="36292-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="36292-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="36292-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="36292-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="36292-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="36292-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="36292-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="36292-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="36292-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="36292-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="36292-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="36292-352">se crea el destino de Hola carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="36292-352">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="36292-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="36292-353">Folder1</span></span><br/><span data-ttu-id="36292-354">&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 + File3 + File4 + File 5 se combina en un archivo con un nombre de archivo generado automáticamente</span><span class="sxs-lookup"><span data-stu-id="36292-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="36292-355">false</span><span class="sxs-lookup"><span data-stu-id="36292-355">false</span></span> |<span data-ttu-id="36292-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="36292-356">preserveHierarchy</span></span> |<span data-ttu-id="36292-357">Para una carpeta de origen carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="36292-357">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="36292-358">Folder1</span><span class="sxs-lookup"><span data-stu-id="36292-358">Folder1</span></span><br/><span data-ttu-id="36292-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="36292-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="36292-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="36292-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="36292-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="36292-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="36292-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="36292-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="36292-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="36292-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="36292-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="36292-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="36292-365">se crea la carpeta de destino de Hello carpeta1 con hello siguiendo estructura</span><span class="sxs-lookup"><span data-stu-id="36292-365">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="36292-366">Folder1</span><span class="sxs-lookup"><span data-stu-id="36292-366">Folder1</span></span><br/><span data-ttu-id="36292-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="36292-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="36292-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="36292-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="36292-369">No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="36292-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="36292-370">false</span><span class="sxs-lookup"><span data-stu-id="36292-370">false</span></span> |<span data-ttu-id="36292-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="36292-371">flattenHierarchy</span></span> |<span data-ttu-id="36292-372">Para una carpeta de origen carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="36292-372">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="36292-373">Folder1</span><span class="sxs-lookup"><span data-stu-id="36292-373">Folder1</span></span><br/><span data-ttu-id="36292-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="36292-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="36292-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="36292-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="36292-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="36292-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="36292-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="36292-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="36292-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="36292-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="36292-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="36292-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="36292-380">se crea la carpeta de destino de Hello carpeta1 con hello siguiendo estructura</span><span class="sxs-lookup"><span data-stu-id="36292-380">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="36292-381">Folder1</span><span class="sxs-lookup"><span data-stu-id="36292-381">Folder1</span></span><br/><span data-ttu-id="36292-382">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="36292-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="36292-383">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2</span><span class="sxs-lookup"><span data-stu-id="36292-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="36292-384">No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="36292-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="36292-385">false</span><span class="sxs-lookup"><span data-stu-id="36292-385">false</span></span> |<span data-ttu-id="36292-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="36292-386">mergeFiles</span></span> |<span data-ttu-id="36292-387">Para una carpeta de origen carpeta1 con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="36292-387">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="36292-388">Folder1</span><span class="sxs-lookup"><span data-stu-id="36292-388">Folder1</span></span><br/><span data-ttu-id="36292-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="36292-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="36292-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="36292-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="36292-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="36292-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="36292-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="36292-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="36292-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="36292-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="36292-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="36292-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="36292-395">se crea la carpeta de destino de Hello carpeta1 con hello siguiendo estructura</span><span class="sxs-lookup"><span data-stu-id="36292-395">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="36292-396">Folder1</span><span class="sxs-lookup"><span data-stu-id="36292-396">Folder1</span></span><br/><span data-ttu-id="36292-397">&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 se combina en un archivo con un nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="36292-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="36292-398">Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="36292-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="36292-399">No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="36292-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="36292-400">Formatos de archivo y de compresión admitidos</span><span class="sxs-lookup"><span data-stu-id="36292-400">Supported file and compression formats</span></span>
<span data-ttu-id="36292-401">Para obtener más información, vea hello [compresión de archivos y formatos de factoría de datos de Azure](data-factory-supported-file-and-compression-formats.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="36292-401">For details, see hello [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a><span data-ttu-id="36292-402">Ejemplos JSON para copiar datos tooand de almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="36292-402">JSON examples for copying data tooand from Data Lake Store</span></span>
<span data-ttu-id="36292-403">Hello en los ejemplos siguientes proporciona definiciones de JSON de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="36292-403">hello following examples provide sample JSON definitions.</span></span> <span data-ttu-id="36292-404">Puede usar estos toocreate de definiciones de ejemplo una canalización mediante hello [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="36292-404">You can use these sample definitions toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="36292-405">Hola ejemplos se muestra cómo toocopy tooand de datos desde el almacenamiento de blobs de Azure y de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="36292-405">hello examples show how toocopy data tooand from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="36292-406">Sin embargo, se pueden copiar datos _directamente_ desde cualquiera de hello orígenes tooany de receptores de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="36292-406">However, data can be copied _directly_ from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="36292-407">Para obtener más información, consulte sección de Hola "almacenes de datos admitidos y formatos" Hola [mover datos mediante la actividad de copia](data-factory-data-movement-activities.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="36292-407">For more information, see hello section "Supported data stores and formats" in hello [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a><span data-ttu-id="36292-408">Ejemplo: Copiar los datos de almacenamiento de blobs de Azure tooAzure almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="36292-408">Example: Copy data from Azure Blob Storage tooAzure Data Lake Store</span></span>
<span data-ttu-id="36292-409">Muestra el código de ejemplo de Hola en esta sección:</span><span class="sxs-lookup"><span data-stu-id="36292-409">hello example code in this section shows:</span></span>

* <span data-ttu-id="36292-410">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="36292-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="36292-411">Un servicio vinculado de tipo [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="36292-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="36292-412">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="36292-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="36292-413">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="36292-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="36292-414">Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="36292-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="36292-415">Hello ejemplos muestran cómo series temporales datos desde almacenamiento de blobs de Azure están copiar tooData Lake almacén cada hora.</span><span class="sxs-lookup"><span data-stu-id="36292-415">hello examples show how time-series data from Azure Blob Storage is copied tooData Lake Store every hour.</span></span> 

<span data-ttu-id="36292-416">**Servicio vinculado de Almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="36292-416">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="36292-417">**Servicio vinculado de Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="36292-417">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="36292-418">Para obtener detalles de configuración, vea hello [vinculado propiedades del servicio](#linked-service-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="36292-418">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="36292-419">**Conjunto de datos de entrada de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="36292-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="36292-420">En el siguiente ejemplo de Hola, datos recoge de un blob nuevo cada hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="36292-420">In hello following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="36292-421">Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="36292-421">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="36292-422">ruta de acceso de carpeta de Hello usa Hola año, mes y parte de día de la hora de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-422">hello folder path uses hello year, month, and day portion of hello start time.</span></span> <span data-ttu-id="36292-423">nombre de archivo de Hello usa hora Hola parte del programa Hola a la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="36292-423">hello file name uses hello hour portion of hello start time.</span></span> <span data-ttu-id="36292-424">Hola `"external": true` configuración indica el servicio de factoría de datos de hello esa tabla hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-424">hello `"external": true` setting informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="36292-425">**Conjunto de datos de salida de Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="36292-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="36292-426">Hola siguiente ejemplo copia datos tooData Lake almacén.</span><span class="sxs-lookup"><span data-stu-id="36292-426">hello following example copies data tooData Lake Store.</span></span> <span data-ttu-id="36292-427">Se copian los datos nuevos tooData Lake almacén cada hora.</span><span class="sxs-lookup"><span data-stu-id="36292-427">New data is copied tooData Lake Store every hour.</span></span>

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


<span data-ttu-id="36292-428">**Actividad de copia en una canalización con un origen de blob y el receptor de Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="36292-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="36292-429">En el siguiente ejemplo de Hola, canalización de hello contiene una actividad de copia que se configura toouse Hola conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="36292-429">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="36292-430">actividad de copia de Hello es toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="36292-430">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="36292-431">En la definición de JSON de canalización de hello, Hola `source` tipo está establecido demasiado`BlobSource`, hello y `sink` tipo está establecido demasiado`AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="36292-431">In hello pipeline JSON definition, hello `source` type is set too`BlobSource`, and hello `sink` type is set too`AzureDataLakeStoreSink`.</span></span>

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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a><span data-ttu-id="36292-432">Ejemplo: Copiar los datos de almacén de Azure Data Lake tooan blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="36292-432">Example: Copy data from Azure Data Lake Store tooan Azure blob</span></span>
<span data-ttu-id="36292-433">Muestra el código de ejemplo de Hola en esta sección:</span><span class="sxs-lookup"><span data-stu-id="36292-433">hello example code in this section shows:</span></span>

* <span data-ttu-id="36292-434">Un servicio vinculado de tipo [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="36292-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="36292-435">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="36292-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="36292-436">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="36292-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="36292-437">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="36292-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="36292-438">Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [AzureDataLakeStoreSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="36292-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="36292-439">código de Hello copia datos de serie temporal de almacén de Data Lake tooan blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="36292-439">hello code copies time-series data from Data Lake Store tooan Azure blob every hour.</span></span> 

<span data-ttu-id="36292-440">**Servicio vinculado de Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="36292-440">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="36292-441">Para obtener detalles de configuración, vea hello [vinculado propiedades del servicio](#linked-service-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="36292-441">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="36292-442">**Servicio vinculado de Almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="36292-442">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="36292-443">**Conjunto de datos de entrada de Azure Data Lake**</span><span class="sxs-lookup"><span data-stu-id="36292-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="36292-444">En este ejemplo, si se establece `"external"` demasiado`true` informa a servicio de factoría de datos de hello esa tabla hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-444">In this example, setting `"external"` too`true` informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="36292-445">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="36292-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="36292-446">En el siguiente ejemplo de Hola, se escriben datos tooa nuevo blob cada hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="36292-446">In hello following example, data is written tooa new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="36292-447">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="36292-447">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="36292-448">ruta de acceso de carpeta de Hello usa Hola año, mes, día y parte de horas de la hora de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="36292-448">hello folder path uses hello year, month, day, and hours portion of hello start time.</span></span>

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

<span data-ttu-id="36292-449">**Una actividad de copia en una canalización con un origen de Azure Data Lake Store y un receptor de blob**</span><span class="sxs-lookup"><span data-stu-id="36292-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="36292-450">En el siguiente ejemplo de Hola, canalización de hello contiene una actividad de copia que se configura toouse Hola conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="36292-450">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="36292-451">actividad de copia de Hello es toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="36292-451">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="36292-452">En la definición de JSON de canalización de hello, Hola `source` tipo está establecido demasiado`AzureDataLakeStoreSource`, hello y `sink` tipo está establecido demasiado`BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="36292-452">In hello pipeline JSON definition, hello `source` type is set too`AzureDataLakeStoreSource`, and hello `sink` type is set too`BlobSink`.</span></span>

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

<span data-ttu-id="36292-453">En la definición de la actividad de copia de hello, también puede asignar columnas de hello toocolumns de conjunto de datos de origen en el conjunto de datos de hello receptor.</span><span class="sxs-lookup"><span data-stu-id="36292-453">In hello copy activity definition, you can also map columns from hello source dataset toocolumns in hello sink dataset.</span></span> <span data-ttu-id="36292-454">Para obtener más información, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="36292-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="36292-455">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="36292-455">Performance and tuning</span></span>
<span data-ttu-id="36292-456">toolearn acerca de los factores de Hola que afectan al rendimiento de la actividad de copia y cómo toooptimize, vea hello [actividad de copia Guía de rendimiento y optimización](data-factory-copy-activity-performance.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="36292-456">toolearn about hello factors that affect Copy Activity performance and how toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
