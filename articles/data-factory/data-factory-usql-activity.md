---
title: datos de aaaTransform mediante script U-SQL - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo el servicio de proceso tooprocess o transformar datos mediante la ejecución de secuencias de comandos SQL U en análisis de Data Lake de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="19ae9-103">Transformación de datos mediante la ejecución de scripts de U-SQL en Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="19ae9-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="19ae9-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="19ae9-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="19ae9-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="19ae9-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="19ae9-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="19ae9-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="19ae9-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="19ae9-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="19ae9-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="19ae9-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="19ae9-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="19ae9-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="19ae9-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="19ae9-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="19ae9-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="19ae9-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="19ae9-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="19ae9-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="19ae9-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="19ae9-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="19ae9-114">Una canalización en una factoría de datos de Azure procesa los datos de los servicios de almacenamiento vinculados mediante el uso de servicios de proceso vinculados.</span><span class="sxs-lookup"><span data-stu-id="19ae9-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="19ae9-115">Contiene una secuencia de actividades donde cada actividad realiza una operación de procesamiento específica.</span><span class="sxs-lookup"><span data-stu-id="19ae9-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="19ae9-116">Este artículo describen hello **actividad de U-SQL de análisis de datos Lake** que se ejecuta un **U-SQL** script en un **análisis de Azure Data Lake** servicio vinculado de proceso.</span><span class="sxs-lookup"><span data-stu-id="19ae9-116">This article describes hello **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="19ae9-117">Debe crear una cuenta de Azure Data Lake Analytics antes de crear una canalización con una actividad de U-SQL de este servicio.</span><span class="sxs-lookup"><span data-stu-id="19ae9-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="19ae9-118">toolearn sobre análisis de Data Lake de Azure, consulte [empezar a trabajar con análisis de Azure Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="19ae9-118">toolearn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="19ae9-119">Hola de revisión [crear su primer tutorial de canalización](data-factory-build-your-first-pipeline.md) para conocer los pasos detallados toocreate una factoría de datos, servicios vinculados, conjuntos de datos y una canalización.</span><span class="sxs-lookup"><span data-stu-id="19ae9-119">Review hello [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps toocreate a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="19ae9-120">Usar fragmentos de JSON con el Editor de generador de datos o entidades de factoría de datos de toocreate de Visual Studio o PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="19ae9-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell toocreate Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="19ae9-121">Tipos de autenticación que se admiten</span><span class="sxs-lookup"><span data-stu-id="19ae9-121">Supported authentication types</span></span>
<span data-ttu-id="19ae9-122">La actividad de U-SQL admite siguientes tipos de autenticación frente a Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="19ae9-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="19ae9-123">Autenticación de entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="19ae9-123">Service principal authentication</span></span>
* <span data-ttu-id="19ae9-124">Autenticación de credenciales de usuario (OAuth)</span><span class="sxs-lookup"><span data-stu-id="19ae9-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="19ae9-125">Se recomienda usar la autenticación de la entidad de servicio, en especial para una ejecución de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="19ae9-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="19ae9-126">Con la autenticación se credenciales de usuario puede darse la situación de que expiren los tokens.</span><span class="sxs-lookup"><span data-stu-id="19ae9-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="19ae9-127">Para obtener detalles de configuración, vea hello [vinculado propiedades del servicio](#azure-data-lake-analytics-linked-service) sección.</span><span class="sxs-lookup"><span data-stu-id="19ae9-127">For configuration details, see hello [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="19ae9-128">Servicio vinculado con el Análisis con Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="19ae9-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="19ae9-129">Crear un **análisis de Azure Data Lake** vinculado toolink un generador de datos de Azure análisis de Azure Data Lake tooan de servicio de proceso de servicio.</span><span class="sxs-lookup"><span data-stu-id="19ae9-129">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory.</span></span> <span data-ttu-id="19ae9-130">actividad de Data Lake Analytics U-SQL en la canalización de Hola Hola hace referencia servicio toothis vinculado.</span><span class="sxs-lookup"><span data-stu-id="19ae9-130">hello Data Lake Analytics U-SQL activity in hello pipeline refers toothis linked service.</span></span> 

<span data-ttu-id="19ae9-131">Hello tabla siguiente ofrece descripciones de hello genéricos propiedades utilizadas en hello definición de JSON.</span><span class="sxs-lookup"><span data-stu-id="19ae9-131">hello following table provides descriptions for hello generic properties used in hello JSON definition.</span></span> <span data-ttu-id="19ae9-132">Puede elegir entre la autenticación de la entidad de servicio y la autenticación de credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="19ae9-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="19ae9-133">Propiedad</span><span class="sxs-lookup"><span data-stu-id="19ae9-133">Property</span></span> | <span data-ttu-id="19ae9-134">Descripción</span><span class="sxs-lookup"><span data-stu-id="19ae9-134">Description</span></span> | <span data-ttu-id="19ae9-135">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19ae9-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19ae9-136">**type**</span><span class="sxs-lookup"><span data-stu-id="19ae9-136">**type**</span></span> |<span data-ttu-id="19ae9-137">propiedad de tipo Hello debe establecerse en: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="19ae9-137">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="19ae9-138">Sí</span><span class="sxs-lookup"><span data-stu-id="19ae9-138">Yes</span></span> |
| <span data-ttu-id="19ae9-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="19ae9-139">**accountName**</span></span> |<span data-ttu-id="19ae9-140">Nombre de la cuenta de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="19ae9-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="19ae9-141">Sí</span><span class="sxs-lookup"><span data-stu-id="19ae9-141">Yes</span></span> |
| <span data-ttu-id="19ae9-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="19ae9-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="19ae9-143">Identificador URI de Análisis de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="19ae9-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="19ae9-144">No</span><span class="sxs-lookup"><span data-stu-id="19ae9-144">No</span></span> |
| <span data-ttu-id="19ae9-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="19ae9-145">**subscriptionId**</span></span> |<span data-ttu-id="19ae9-146">Identificador de suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="19ae9-146">Azure subscription id</span></span> |<span data-ttu-id="19ae9-147">No (si no se especifica, suscripción de Hola se usa la factoría de datos).</span><span class="sxs-lookup"><span data-stu-id="19ae9-147">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="19ae9-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="19ae9-148">**resourceGroupName**</span></span> |<span data-ttu-id="19ae9-149">Nombre del grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="19ae9-149">Azure resource group name</span></span> |<span data-ttu-id="19ae9-150">No (si no se especifica, el grupo de recursos de Hola se usa la factoría de datos).</span><span class="sxs-lookup"><span data-stu-id="19ae9-150">No (If not specified, resource group of hello data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="19ae9-151">Autenticación de la entidad de servicio (recomendada)</span><span class="sxs-lookup"><span data-stu-id="19ae9-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="19ae9-152">toouse autenticación principal del servicio, registrar una entidad de la aplicación en Azure Active Directory (Azure AD) y conceda a Hola acceso tooData Lake almacén.</span><span class="sxs-lookup"><span data-stu-id="19ae9-152">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="19ae9-153">Consulte [Autenticación entre servicios](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) para ver los pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="19ae9-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="19ae9-154">Tome nota de hello después de valores, que se utiliza toodefine Hola servicio vinculado:</span><span class="sxs-lookup"><span data-stu-id="19ae9-154">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="19ae9-155">Identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="19ae9-155">Application ID</span></span>
* <span data-ttu-id="19ae9-156">Clave de la aplicación</span><span class="sxs-lookup"><span data-stu-id="19ae9-156">Application key</span></span> 
* <span data-ttu-id="19ae9-157">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="19ae9-157">Tenant ID</span></span>

<span data-ttu-id="19ae9-158">Utilizar autenticación de entidad de seguridad de servicio mediante la especificación de hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="19ae9-158">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="19ae9-159">Propiedad</span><span class="sxs-lookup"><span data-stu-id="19ae9-159">Property</span></span> | <span data-ttu-id="19ae9-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="19ae9-160">Description</span></span> | <span data-ttu-id="19ae9-161">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19ae9-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="19ae9-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="19ae9-162">**servicePrincipalId**</span></span> | <span data-ttu-id="19ae9-163">Especifique el identificador de cliente de. la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="19ae9-163">Specify hello application's client ID.</span></span> | <span data-ttu-id="19ae9-164">Sí</span><span class="sxs-lookup"><span data-stu-id="19ae9-164">Yes</span></span> |
| <span data-ttu-id="19ae9-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="19ae9-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="19ae9-166">Especifique la clave de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="19ae9-166">Specify hello application's key.</span></span> | <span data-ttu-id="19ae9-167">Sí</span><span class="sxs-lookup"><span data-stu-id="19ae9-167">Yes</span></span> |
| <span data-ttu-id="19ae9-168">**tenant**</span><span class="sxs-lookup"><span data-stu-id="19ae9-168">**tenant**</span></span> | <span data-ttu-id="19ae9-169">Especifique la información de inquilino de hello (inquilino o el nombre de identificador de dominio) en que se encuentra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="19ae9-169">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="19ae9-170">Puede recuperarlo mediante el desplazamiento del mouse de hello en la esquina superior derecha de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="19ae9-170">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="19ae9-171">Sí</span><span class="sxs-lookup"><span data-stu-id="19ae9-171">Yes</span></span> |

<span data-ttu-id="19ae9-172">**Ejemplo: autenticación de la entidad de servicio**</span><span class="sxs-lookup"><span data-stu-id="19ae9-172">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="19ae9-173">Autenticación de credenciales de usuario</span><span class="sxs-lookup"><span data-stu-id="19ae9-173">User credential authentication</span></span>
<span data-ttu-id="19ae9-174">Como alternativa, puede usar la autenticación de credenciales de usuario para el análisis de Data Lake especificando Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="19ae9-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying hello following properties:</span></span>

| <span data-ttu-id="19ae9-175">Propiedad</span><span class="sxs-lookup"><span data-stu-id="19ae9-175">Property</span></span> | <span data-ttu-id="19ae9-176">Descripción</span><span class="sxs-lookup"><span data-stu-id="19ae9-176">Description</span></span> | <span data-ttu-id="19ae9-177">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19ae9-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="19ae9-178">**authorization**</span><span class="sxs-lookup"><span data-stu-id="19ae9-178">**authorization**</span></span> | <span data-ttu-id="19ae9-179">Haga clic en hello **Authorize** botón Hola Editor de generador de datos y escriba sus credenciales que asigna la propiedad de hello autogenerado autorización URL toothis.</span><span class="sxs-lookup"><span data-stu-id="19ae9-179">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="19ae9-180">Sí</span><span class="sxs-lookup"><span data-stu-id="19ae9-180">Yes</span></span> |
| <span data-ttu-id="19ae9-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="19ae9-181">**sessionId**</span></span> | <span data-ttu-id="19ae9-182">Identificador de sesión de OAuth de sesión de autorización de OAuth de Hola.</span><span class="sxs-lookup"><span data-stu-id="19ae9-182">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="19ae9-183">Cada id. de sesión es único y solo se puede usar una vez.</span><span class="sxs-lookup"><span data-stu-id="19ae9-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="19ae9-184">Esta configuración se genera automáticamente cuando se usa Hola Editor de generador de datos.</span><span class="sxs-lookup"><span data-stu-id="19ae9-184">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="19ae9-185">Sí</span><span class="sxs-lookup"><span data-stu-id="19ae9-185">Yes</span></span> |

<span data-ttu-id="19ae9-186">**Ejemplo: autenticación de credenciales de usuario**</span><span class="sxs-lookup"><span data-stu-id="19ae9-186">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="19ae9-187">Expiración del token</span><span class="sxs-lookup"><span data-stu-id="19ae9-187">Token expiration</span></span>
<span data-ttu-id="19ae9-188">Hola código de autorización ha generado mediante el uso de hello **Authorize** botón expira después de unos minutos.</span><span class="sxs-lookup"><span data-stu-id="19ae9-188">hello authorization code you generated by using hello **Authorize** button expires after sometime.</span></span> <span data-ttu-id="19ae9-189">Vea hello en la tabla siguiente para unos tiempos de expiración Hola para diferentes tipos de cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="19ae9-189">See hello following table for hello expiration times for different types of user accounts.</span></span> <span data-ttu-id="19ae9-190">Es posible que vea Hola mensaje de error siguiente cuando Hola autenticación **expira el token**: error de operación de credenciales: concesión_no_válida - AADSTS70002: Error al validar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="19ae9-190">You may see hello following error message when hello authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="19ae9-191">AADSTS70008: Hola proporciona concesión de acceso expiró o se revocó.</span><span class="sxs-lookup"><span data-stu-id="19ae9-191">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="19ae9-192">Id. de seguimiento: d18629e8-af88-43c5-88e3-d8419eb1fca1 Id. de correlación: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Marca de tiempo: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="19ae9-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="19ae9-193">Tipo de usuario</span><span class="sxs-lookup"><span data-stu-id="19ae9-193">User type</span></span> | <span data-ttu-id="19ae9-194">Expira después de</span><span class="sxs-lookup"><span data-stu-id="19ae9-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="19ae9-195">Cuentas de usuario NO administradas por Azure Active Directory (@hotmail.com, @live.com, etc.)</span><span class="sxs-lookup"><span data-stu-id="19ae9-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="19ae9-196">12 horas</span><span class="sxs-lookup"><span data-stu-id="19ae9-196">12 hours</span></span> |
| <span data-ttu-id="19ae9-197">Cuentas de usuario administradas por Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="19ae9-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="19ae9-198">Ejecute 14 días después de último segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="19ae9-198">14 days after hello last slice run.</span></span> <br/><br/><span data-ttu-id="19ae9-199">Noventa días, si un segmento basado en el servicio vinculado basado en OAuth se ejecuta al menos una vez cada catorce días.</span><span class="sxs-lookup"><span data-stu-id="19ae9-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="19ae9-200">tooavoid/resolve este error, volver a autorizar mediante hello **Authorize** botón cuando hello **expira el token** y vuelva a implementar el servicio de hello vinculado.</span><span class="sxs-lookup"><span data-stu-id="19ae9-200">tooavoid/resolve this error, reauthorize using hello **Authorize** button when hello **token expires** and redeploy hello linked service.</span></span> <span data-ttu-id="19ae9-201">También puede generar valores para las propiedades **sessionId** y **authorization** mediante programación, para lo que usará el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="19ae9-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="19ae9-202">Vea [azuredatalakestorelinkedservice clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), y [AuthorizationSessionGetResponse clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) temas para obtener más información acerca de clases de factoría de datos de hello utilizadas en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="19ae9-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about hello Data Factory classes used in hello code.</span></span> <span data-ttu-id="19ae9-203">Agregue una referencia a: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll para hello WindowsFormsWebAuthenticationDialog clase.</span><span class="sxs-lookup"><span data-stu-id="19ae9-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for hello WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="19ae9-204">Actividad U-SQL de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="19ae9-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="19ae9-205">Hola siguiente fragmento JSON define una canalización con la actividad de U-SQL de análisis de datos Lake.</span><span class="sxs-lookup"><span data-stu-id="19ae9-205">hello following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="19ae9-206">definición de actividad de Hello tiene un servicio de análisis de Azure Data Lake vinculado que creó anteriormente toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="19ae9-206">hello activity definition has a reference toohello Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="19ae9-207">Hello tabla siguiente describen nombres y descripciones de propiedades de actividad toothis específico.</span><span class="sxs-lookup"><span data-stu-id="19ae9-207">hello following table describes names and descriptions of properties that are specific toothis activity.</span></span> 

| <span data-ttu-id="19ae9-208">Propiedad</span><span class="sxs-lookup"><span data-stu-id="19ae9-208">Property</span></span> | <span data-ttu-id="19ae9-209">Descripción</span><span class="sxs-lookup"><span data-stu-id="19ae9-209">Description</span></span> | <span data-ttu-id="19ae9-210">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19ae9-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="19ae9-211">type</span><span class="sxs-lookup"><span data-stu-id="19ae9-211">type</span></span> |<span data-ttu-id="19ae9-212">se debe establecer propiedad de tipo Hello demasiado**DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="19ae9-212">hello type property must be set too**DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="19ae9-213">Sí</span><span class="sxs-lookup"><span data-stu-id="19ae9-213">Yes</span></span> |
| <span data-ttu-id="19ae9-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="19ae9-214">scriptPath</span></span> |<span data-ttu-id="19ae9-215">Toofolder de ruta de acceso que contiene el script de Hola U-SQL.</span><span class="sxs-lookup"><span data-stu-id="19ae9-215">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="19ae9-216">Nombre del archivo hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="19ae9-216">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="19ae9-217">No (si se utiliza el script)</span><span class="sxs-lookup"><span data-stu-id="19ae9-217">No (if you use script)</span></span> |
| <span data-ttu-id="19ae9-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="19ae9-218">scriptLinkedService</span></span> |<span data-ttu-id="19ae9-219">Servicio vinculado que se vincula el almacenamiento de Hola que contiene la factoría de datos de hello script toohello</span><span class="sxs-lookup"><span data-stu-id="19ae9-219">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="19ae9-220">No (si se utiliza el script)</span><span class="sxs-lookup"><span data-stu-id="19ae9-220">No (if you use script)</span></span> |
| <span data-ttu-id="19ae9-221">script</span><span class="sxs-lookup"><span data-stu-id="19ae9-221">script</span></span> |<span data-ttu-id="19ae9-222">Especifique el script en línea en lugar de scriptPath y scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="19ae9-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="19ae9-223">Por ejemplo: `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="19ae9-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="19ae9-224">No (si usa scriptPath y scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="19ae9-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="19ae9-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="19ae9-225">degreeOfParallelism</span></span> |<span data-ttu-id="19ae9-226">número máximo de Hola de nodos simultáneamente utiliza trabajo de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="19ae9-226">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="19ae9-227">No</span><span class="sxs-lookup"><span data-stu-id="19ae9-227">No</span></span> |
| <span data-ttu-id="19ae9-228">prioridad</span><span class="sxs-lookup"><span data-stu-id="19ae9-228">priority</span></span> |<span data-ttu-id="19ae9-229">Determina qué trabajos de todos los que se ponen en cola deberían estar seleccionado toorun en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="19ae9-229">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="19ae9-230">Hola Hola número inferior, prioridad Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="19ae9-230">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="19ae9-231">No</span><span class="sxs-lookup"><span data-stu-id="19ae9-231">No</span></span> |
| <span data-ttu-id="19ae9-232">parameters</span><span class="sxs-lookup"><span data-stu-id="19ae9-232">parameters</span></span> |<span data-ttu-id="19ae9-233">Parámetros de script de Hola U-SQL</span><span class="sxs-lookup"><span data-stu-id="19ae9-233">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="19ae9-234">No</span><span class="sxs-lookup"><span data-stu-id="19ae9-234">No</span></span> |
| <span data-ttu-id="19ae9-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="19ae9-235">runtimeVersion</span></span> | <span data-ttu-id="19ae9-236">Versión del Runtime de hello U-SQL motor toouse</span><span class="sxs-lookup"><span data-stu-id="19ae9-236">Runtime version of hello U-SQL engine toouse</span></span> | <span data-ttu-id="19ae9-237">No</span><span class="sxs-lookup"><span data-stu-id="19ae9-237">No</span></span> | 
| <span data-ttu-id="19ae9-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="19ae9-238">compilationMode</span></span> | <p><span data-ttu-id="19ae9-239">Modo de compilación de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="19ae9-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="19ae9-240">Debe ser uno de los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="19ae9-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="19ae9-241">**Semantic:** solo realiza comprobaciones semánticas y comprobaciones de integridad necesarias.</span><span class="sxs-lookup"><span data-stu-id="19ae9-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="19ae9-242">**Completo:** realizar Hola completos de la compilación, incluida la comprobación de sintaxis, optimización, generación de código, etcetera.</span><span class="sxs-lookup"><span data-stu-id="19ae9-242">**Full:** Perform hello full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="19ae9-243">**SingleBox:** realizar Hola completos de la compilación, con TargetType configuración tooSingleBox.</span><span class="sxs-lookup"><span data-stu-id="19ae9-243">**SingleBox:** Perform hello full compilation, with TargetType setting tooSingleBox.</span></span></li></ul><p><span data-ttu-id="19ae9-244">Si no especifica un valor para esta propiedad, servidor hello determina el modo de compilación óptimo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19ae9-244">If you don't specify a value for this property, hello server determines hello optimal compilation mode.</span></span> </p>| <span data-ttu-id="19ae9-245">No</span><span class="sxs-lookup"><span data-stu-id="19ae9-245">No</span></span> | 

<span data-ttu-id="19ae9-246">Vea [SearchLogProcessing.txt Script definición](#sample-u-sql-script) para la definición de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="19ae9-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for hello script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="19ae9-247">Conjuntos de datos de entrada y salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="19ae9-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="19ae9-248">Conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="19ae9-248">Input dataset</span></span>
<span data-ttu-id="19ae9-249">En este ejemplo, los datos de entrada de hello residen en un almacén de Azure Data Lake (archivo de SearchLog.tsv de carpeta de entrada/datalake Hola).</span><span class="sxs-lookup"><span data-stu-id="19ae9-249">In this example, hello input data resides in an Azure Data Lake Store (SearchLog.tsv file in hello datalake/input folder).</span></span> 

```json
{
    "name": "DataLakeTable",
    "properties": {
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
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a><span data-ttu-id="19ae9-250">Conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="19ae9-250">Output dataset</span></span>
<span data-ttu-id="19ae9-251">En este ejemplo, los datos de salida de hello generados por script U-SQL Hola se almacenan en un almacén de Azure Data Lake (carpeta de datalake/salida).</span><span class="sxs-lookup"><span data-stu-id="19ae9-251">In this example, hello output data produced by hello U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="19ae9-252">Ejemplo de servicio vinculado de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="19ae9-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="19ae9-253">Aquí es definición de Hola de ejemplo de Hola a que almacén de Azure Data Lake vinculado servicio utilizado por los conjuntos de datos de entrada/salida de hello.</span><span class="sxs-lookup"><span data-stu-id="19ae9-253">Here is hello definition of hello sample Azure Data Lake Store linked service used by hello input/output datasets.</span></span> 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

<span data-ttu-id="19ae9-254">Vea [mover tooand de datos de almacén de Azure Data Lake](data-factory-azure-datalake-connector.md) artículo para obtener descripciones de propiedades JSON.</span><span class="sxs-lookup"><span data-stu-id="19ae9-254">See [Move data tooand from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="19ae9-255">Script U-SQL</span><span class="sxs-lookup"><span data-stu-id="19ae9-255">Sample U-SQL Script</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="19ae9-256">Hola valores para  **@in**  y  **@out**  parámetros en el script de Hola U-SQL se pasan dinámicamente por ADF mediante hello 'parameters' sección.</span><span class="sxs-lookup"><span data-stu-id="19ae9-256">hello values for **@in** and **@out** parameters in hello U-SQL script are passed dynamically by ADF using hello ‘parameters’ section.</span></span> <span data-ttu-id="19ae9-257">Vea la sección de "parámetros" de hello en la definición de la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="19ae9-257">See hello ‘parameters’ section in hello pipeline definition.</span></span>

<span data-ttu-id="19ae9-258">También puede especificar otras propiedades, como degreeOfParallelism y la prioridad en la definición de canalización para los trabajos de Hola que se ejecutan en el servicio de análisis de Azure Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="19ae9-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for hello jobs that run on hello Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="19ae9-259">Parámetros dinámicos</span><span class="sxs-lookup"><span data-stu-id="19ae9-259">Dynamic parameters</span></span>
<span data-ttu-id="19ae9-260">En la definición de la canalización de ejemplo de Hola, los parámetros de entrada y salida se asignan con valores codificados de forma rígida.</span><span class="sxs-lookup"><span data-stu-id="19ae9-260">In hello sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="19ae9-261">Es posible toouse los parámetros dinámicos en su lugar.</span><span class="sxs-lookup"><span data-stu-id="19ae9-261">It is possible toouse dynamic parameters instead.</span></span> <span data-ttu-id="19ae9-262">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="19ae9-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="19ae9-263">En este caso, todavía se recogen los archivos de entrada desde la carpeta de /datalake/input de Hola y archivos de salida se generan en la carpeta de /datalake/output Hola.</span><span class="sxs-lookup"><span data-stu-id="19ae9-263">In this case, input files are still picked up from hello /datalake/input folder and output files are generated in hello /datalake/output folder.</span></span> <span data-ttu-id="19ae9-264">nombres de archivo de Hello son dinámicos en función de la hora de inicio del segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="19ae9-264">hello file names are dynamic based on hello slice start time.</span></span>  

