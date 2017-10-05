---
title: "Transformación de datos mediante un script de U-SQL - Azure | Microsoft Docs"
description: "Aprenda a procesar o transformar datos mediante la ejecución de scripts de U-SQL en el servicio de proceso Azure Data Lake Analytics."
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
ms.openlocfilehash: 49a809af92ed1bc6664fbdd3bf1aabf36afb8180
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="1bf17-103">Transformación de datos mediante la ejecución de scripts de U-SQL en Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1bf17-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="1bf17-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="1bf17-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="1bf17-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="1bf17-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="1bf17-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="1bf17-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="1bf17-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="1bf17-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="1bf17-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="1bf17-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="1bf17-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1bf17-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="1bf17-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1bf17-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="1bf17-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="1bf17-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="1bf17-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1bf17-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="1bf17-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="1bf17-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="1bf17-114">Una canalización en una factoría de datos de Azure procesa los datos de los servicios de almacenamiento vinculados mediante el uso de servicios de proceso vinculados.</span><span class="sxs-lookup"><span data-stu-id="1bf17-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="1bf17-115">Contiene una secuencia de actividades donde cada actividad realiza una operación de procesamiento específica.</span><span class="sxs-lookup"><span data-stu-id="1bf17-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="1bf17-116">En este artículo se describe la **actividad U-SQL de Data Lake Analytics** que ejecuta un script de **U-SQL** en un servicio vinculado de proceso de **Azure Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="1bf17-116">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="1bf17-117">Debe crear una cuenta de Azure Data Lake Analytics antes de crear una canalización con una actividad de U-SQL de este servicio.</span><span class="sxs-lookup"><span data-stu-id="1bf17-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="1bf17-118">Para obtener más información sobre Azure Data Lake Analytics, consulte el artículo de [introducción a Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1bf17-118">To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="1bf17-119">Revise el [tutorial sobre la compilación de la primera canalización](data-factory-build-your-first-pipeline.md) para ver los pasos detallados para crear una factoría de datos, servicios vinculados, conjuntos de datos y una canalización.</span><span class="sxs-lookup"><span data-stu-id="1bf17-119">Review the [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps to create a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="1bf17-120">Use los fragmentos de código JSON con el Editor de Data Factory, Visual Studio o Azure PowerShell para crear las entidades de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1bf17-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell to create Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="1bf17-121">Tipos de autenticación que se admiten</span><span class="sxs-lookup"><span data-stu-id="1bf17-121">Supported authentication types</span></span>
<span data-ttu-id="1bf17-122">La actividad de U-SQL admite siguientes tipos de autenticación frente a Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="1bf17-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="1bf17-123">Autenticación de entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="1bf17-123">Service principal authentication</span></span>
* <span data-ttu-id="1bf17-124">Autenticación de credenciales de usuario (OAuth)</span><span class="sxs-lookup"><span data-stu-id="1bf17-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="1bf17-125">Se recomienda usar la autenticación de la entidad de servicio, en especial para una ejecución de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1bf17-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="1bf17-126">Con la autenticación se credenciales de usuario puede darse la situación de que expiren los tokens.</span><span class="sxs-lookup"><span data-stu-id="1bf17-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="1bf17-127">Para información sobre los detalles de configuración, consulte la sección [Propiedades del servicio vinculado](#azure-data-lake-analytics-linked-service).</span><span class="sxs-lookup"><span data-stu-id="1bf17-127">For configuration details, see the [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="1bf17-128">Servicio vinculado con el Análisis con Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1bf17-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="1bf17-129">Cree un servicio vinculado de **Azure Data Lake Analytics** para vincular un servicio de proceso de Azure Data Lake Analytics a una instancia de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1bf17-129">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="1bf17-130">La actividad de U-SQL de Data Lake Analytics de la canalización hace referencia a este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1bf17-130">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="1bf17-131">En la siguiente tabla se ofrecen descripciones de las propiedades genéricas que se usan en la definición de JSON.</span><span class="sxs-lookup"><span data-stu-id="1bf17-131">The following table provides descriptions for the generic properties used in the JSON definition.</span></span> <span data-ttu-id="1bf17-132">Puede elegir entre la autenticación de la entidad de servicio y la autenticación de credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="1bf17-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="1bf17-133">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1bf17-133">Property</span></span> | <span data-ttu-id="1bf17-134">Descripción</span><span class="sxs-lookup"><span data-stu-id="1bf17-134">Description</span></span> | <span data-ttu-id="1bf17-135">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1bf17-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1bf17-136">**type**</span><span class="sxs-lookup"><span data-stu-id="1bf17-136">**type**</span></span> |<span data-ttu-id="1bf17-137">La propiedad type se debe establecer en: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="1bf17-137">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="1bf17-138">Sí</span><span class="sxs-lookup"><span data-stu-id="1bf17-138">Yes</span></span> |
| <span data-ttu-id="1bf17-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="1bf17-139">**accountName**</span></span> |<span data-ttu-id="1bf17-140">Nombre de la cuenta de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1bf17-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="1bf17-141">Sí</span><span class="sxs-lookup"><span data-stu-id="1bf17-141">Yes</span></span> |
| <span data-ttu-id="1bf17-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="1bf17-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="1bf17-143">Identificador URI de Análisis de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1bf17-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="1bf17-144">No</span><span class="sxs-lookup"><span data-stu-id="1bf17-144">No</span></span> |
| <span data-ttu-id="1bf17-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="1bf17-145">**subscriptionId**</span></span> |<span data-ttu-id="1bf17-146">Identificador de suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="1bf17-146">Azure subscription id</span></span> |<span data-ttu-id="1bf17-147">No (si no se especifica, se usa la suscripción de Data Factory).</span><span class="sxs-lookup"><span data-stu-id="1bf17-147">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="1bf17-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="1bf17-148">**resourceGroupName**</span></span> |<span data-ttu-id="1bf17-149">Nombre del grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bf17-149">Azure resource group name</span></span> |<span data-ttu-id="1bf17-150">No (si no se especifica, se usa el grupo de recursos de la factoría de datos).</span><span class="sxs-lookup"><span data-stu-id="1bf17-150">No (If not specified, resource group of the data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="1bf17-151">Autenticación de la entidad de servicio (recomendada)</span><span class="sxs-lookup"><span data-stu-id="1bf17-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="1bf17-152">Para usar la autenticación de la entidad de servicio, registre una entidad de aplicación en Azure Active Directory (AAD) y concédale acceso a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1bf17-152">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="1bf17-153">Consulte [Autenticación entre servicios](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) para ver los pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="1bf17-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="1bf17-154">Anote los siguientes valores; los usará para definir el servicio vinculado:</span><span class="sxs-lookup"><span data-stu-id="1bf17-154">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="1bf17-155">Identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="1bf17-155">Application ID</span></span>
* <span data-ttu-id="1bf17-156">Clave de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1bf17-156">Application key</span></span> 
* <span data-ttu-id="1bf17-157">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="1bf17-157">Tenant ID</span></span>

<span data-ttu-id="1bf17-158">Para usar la autenticación de la entidad de servicio, especifique las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="1bf17-158">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="1bf17-159">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1bf17-159">Property</span></span> | <span data-ttu-id="1bf17-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="1bf17-160">Description</span></span> | <span data-ttu-id="1bf17-161">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1bf17-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1bf17-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="1bf17-162">**servicePrincipalId**</span></span> | <span data-ttu-id="1bf17-163">Especifique el id. de cliente de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1bf17-163">Specify the application's client ID.</span></span> | <span data-ttu-id="1bf17-164">Sí</span><span class="sxs-lookup"><span data-stu-id="1bf17-164">Yes</span></span> |
| <span data-ttu-id="1bf17-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="1bf17-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="1bf17-166">Especifique la clave de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1bf17-166">Specify the application's key.</span></span> | <span data-ttu-id="1bf17-167">Sí</span><span class="sxs-lookup"><span data-stu-id="1bf17-167">Yes</span></span> |
| <span data-ttu-id="1bf17-168">**tenant**</span><span class="sxs-lookup"><span data-stu-id="1bf17-168">**tenant**</span></span> | <span data-ttu-id="1bf17-169">Especifique la información del inquilino (nombre de dominio o identificador de inquilino) en el que reside la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1bf17-169">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="1bf17-170">Para recuperarlo, mantenga el puntero del mouse en la esquina superior derecha de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1bf17-170">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="1bf17-171">Sí</span><span class="sxs-lookup"><span data-stu-id="1bf17-171">Yes</span></span> |

<span data-ttu-id="1bf17-172">**Ejemplo: autenticación de la entidad de servicio**</span><span class="sxs-lookup"><span data-stu-id="1bf17-172">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="1bf17-173">Autenticación de credenciales de usuario</span><span class="sxs-lookup"><span data-stu-id="1bf17-173">User credential authentication</span></span>
<span data-ttu-id="1bf17-174">También puede utilizar la autenticación de credenciales de usuario para Data Lake Analytics mediante la especificación de las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="1bf17-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying the following properties:</span></span>

| <span data-ttu-id="1bf17-175">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1bf17-175">Property</span></span> | <span data-ttu-id="1bf17-176">Descripción</span><span class="sxs-lookup"><span data-stu-id="1bf17-176">Description</span></span> | <span data-ttu-id="1bf17-177">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1bf17-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1bf17-178">**authorization**</span><span class="sxs-lookup"><span data-stu-id="1bf17-178">**authorization**</span></span> | <span data-ttu-id="1bf17-179">Haga clic en el botón **Autorizar** de Data Factory Editor y escriba sus credenciales, que asignan la dirección URL de autorización generada automáticamente a esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="1bf17-179">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="1bf17-180">Sí</span><span class="sxs-lookup"><span data-stu-id="1bf17-180">Yes</span></span> |
| <span data-ttu-id="1bf17-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="1bf17-181">**sessionId**</span></span> | <span data-ttu-id="1bf17-182">Id. de sesión de OAuth de la sesión de autorización de OAuth.</span><span class="sxs-lookup"><span data-stu-id="1bf17-182">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="1bf17-183">Cada id. de sesión es único y solo se puede usar una vez.</span><span class="sxs-lookup"><span data-stu-id="1bf17-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="1bf17-184">Esta configuración se genera automáticamente al usar Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="1bf17-184">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="1bf17-185">Sí</span><span class="sxs-lookup"><span data-stu-id="1bf17-185">Yes</span></span> |

<span data-ttu-id="1bf17-186">**Ejemplo: autenticación de credenciales de usuario**</span><span class="sxs-lookup"><span data-stu-id="1bf17-186">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="1bf17-187">Expiración del token</span><span class="sxs-lookup"><span data-stu-id="1bf17-187">Token expiration</span></span>
<span data-ttu-id="1bf17-188">El código de autorización que se generó al hacer clic en el botón **Autorizar** expira poco tiempo después.</span><span class="sxs-lookup"><span data-stu-id="1bf17-188">The authorization code you generated by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="1bf17-189">Consulte la tabla siguiente para conocer el momento en que expiran los distintos tipos de cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="1bf17-189">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="1bf17-190">Puede ver el siguiente mensaje de error cuando el **token de autenticación expira**: Error de operación de credencial: invalid_grant - AADSTS70002: error al validar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="1bf17-190">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="1bf17-191">AADSTS70008: la concesión de acceso proporcionada expiró o se revocó.</span><span class="sxs-lookup"><span data-stu-id="1bf17-191">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="1bf17-192">Id. de seguimiento: d18629e8-af88-43c5-88e3-d8419eb1fca1 Id. de correlación: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Marca de tiempo: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="1bf17-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="1bf17-193">Tipo de usuario</span><span class="sxs-lookup"><span data-stu-id="1bf17-193">User type</span></span> | <span data-ttu-id="1bf17-194">Expira después de</span><span class="sxs-lookup"><span data-stu-id="1bf17-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="1bf17-195">Cuentas de usuario NO administradas por Azure Active Directory (@hotmail.com, @live.com, etc.)</span><span class="sxs-lookup"><span data-stu-id="1bf17-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="1bf17-196">12 horas</span><span class="sxs-lookup"><span data-stu-id="1bf17-196">12 hours</span></span> |
| <span data-ttu-id="1bf17-197">Cuentas de usuario administradas por Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="1bf17-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="1bf17-198">14 días después de la ejecución del último segmento.</span><span class="sxs-lookup"><span data-stu-id="1bf17-198">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="1bf17-199">Noventa días, si un segmento basado en el servicio vinculado basado en OAuth se ejecuta al menos una vez cada catorce días.</span><span class="sxs-lookup"><span data-stu-id="1bf17-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="1bf17-200">Para evitar o resolver este error, vuelva a dar la autorización con el botón **Autorizar** cuando el **token expire** e implemente de nuevo el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="1bf17-200">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="1bf17-201">También puede generar valores para las propiedades **sessionId** y **authorization** mediante programación, para lo que usará el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="1bf17-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="1bf17-202">Para más información sobre las clases de Data Factory que se usan en el código, consulte los temas [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) y [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx).</span><span class="sxs-lookup"><span data-stu-id="1bf17-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="1bf17-203">Agregue una referencia a Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll para la clase WindowsFormsWebAuthenticationDialog.</span><span class="sxs-lookup"><span data-stu-id="1bf17-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="1bf17-204">Actividad U-SQL de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1bf17-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="1bf17-205">El siguiente fragmento JSON define una canalización con una actividad U-SQL de Análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1bf17-205">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="1bf17-206">La definición de actividad tiene una referencia al servicio vinculado de Análisis de Azure Data Lake que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1bf17-206">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline to compute events for en-gb locale and date less than 2012/02/19.",
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

<span data-ttu-id="1bf17-207">En la tabla siguiente se describen los nombres y descripciones de las propiedades que son específicas de esta actividad.</span><span class="sxs-lookup"><span data-stu-id="1bf17-207">The following table describes names and descriptions of properties that are specific to this activity.</span></span> 

| <span data-ttu-id="1bf17-208">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1bf17-208">Property</span></span> | <span data-ttu-id="1bf17-209">Descripción</span><span class="sxs-lookup"><span data-stu-id="1bf17-209">Description</span></span> | <span data-ttu-id="1bf17-210">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1bf17-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1bf17-211">Tipo</span><span class="sxs-lookup"><span data-stu-id="1bf17-211">type</span></span> |<span data-ttu-id="1bf17-212">La propiedad type debe establecerse en **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="1bf17-212">The type property must be set to **DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="1bf17-213">Sí</span><span class="sxs-lookup"><span data-stu-id="1bf17-213">Yes</span></span> |
| <span data-ttu-id="1bf17-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="1bf17-214">scriptPath</span></span> |<span data-ttu-id="1bf17-215">Ruta de acceso a la carpeta que contiene el script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1bf17-215">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="1bf17-216">El nombre del archivo distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="1bf17-216">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="1bf17-217">No (si se utiliza el script)</span><span class="sxs-lookup"><span data-stu-id="1bf17-217">No (if you use script)</span></span> |
| <span data-ttu-id="1bf17-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="1bf17-218">scriptLinkedService</span></span> |<span data-ttu-id="1bf17-219">Servicio vinculado que se vincula al almacenamiento que contiene el script para la factoría de datos</span><span class="sxs-lookup"><span data-stu-id="1bf17-219">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="1bf17-220">No (si se utiliza el script)</span><span class="sxs-lookup"><span data-stu-id="1bf17-220">No (if you use script)</span></span> |
| <span data-ttu-id="1bf17-221">script</span><span class="sxs-lookup"><span data-stu-id="1bf17-221">script</span></span> |<span data-ttu-id="1bf17-222">Especifique el script en línea en lugar de scriptPath y scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="1bf17-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="1bf17-223">Por ejemplo: `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="1bf17-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="1bf17-224">No (si usa scriptPath y scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="1bf17-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="1bf17-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="1bf17-225">degreeOfParallelism</span></span> |<span data-ttu-id="1bf17-226">Número máximo de nodos que se usará de forma simultánea para ejecutar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="1bf17-226">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="1bf17-227">No</span><span class="sxs-lookup"><span data-stu-id="1bf17-227">No</span></span> |
| <span data-ttu-id="1bf17-228">prioridad</span><span class="sxs-lookup"><span data-stu-id="1bf17-228">priority</span></span> |<span data-ttu-id="1bf17-229">Determina qué trabajos de todos los están en cola deben seleccionarse para ejecutarse primero.</span><span class="sxs-lookup"><span data-stu-id="1bf17-229">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="1bf17-230">Cuanto menor sea el número, mayor será la prioridad.</span><span class="sxs-lookup"><span data-stu-id="1bf17-230">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="1bf17-231">No</span><span class="sxs-lookup"><span data-stu-id="1bf17-231">No</span></span> |
| <span data-ttu-id="1bf17-232">parameters</span><span class="sxs-lookup"><span data-stu-id="1bf17-232">parameters</span></span> |<span data-ttu-id="1bf17-233">Parámetros del script SQL U</span><span class="sxs-lookup"><span data-stu-id="1bf17-233">Parameters for the U-SQL script</span></span> |<span data-ttu-id="1bf17-234">No</span><span class="sxs-lookup"><span data-stu-id="1bf17-234">No</span></span> |
| <span data-ttu-id="1bf17-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="1bf17-235">runtimeVersion</span></span> | <span data-ttu-id="1bf17-236">Versión en tiempo de ejecución del motor de U-SQL que se usa</span><span class="sxs-lookup"><span data-stu-id="1bf17-236">Runtime version of the U-SQL engine to use</span></span> | <span data-ttu-id="1bf17-237">No</span><span class="sxs-lookup"><span data-stu-id="1bf17-237">No</span></span> | 
| <span data-ttu-id="1bf17-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="1bf17-238">compilationMode</span></span> | <p><span data-ttu-id="1bf17-239">Modo de compilación de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1bf17-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="1bf17-240">Debe ser uno de los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="1bf17-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="1bf17-241">**Semantic:** solo realiza comprobaciones semánticas y comprobaciones de integridad necesarias.</span><span class="sxs-lookup"><span data-stu-id="1bf17-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="1bf17-242">**Full:** realiza la compilación completa (comprobación de sintaxis, optimización, generación de código, etc.).</span><span class="sxs-lookup"><span data-stu-id="1bf17-242">**Full:** Perform the full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="1bf17-243">**SingleBox:** realiza la compilación completa, con la opción TargetType en SingleBox.</span><span class="sxs-lookup"><span data-stu-id="1bf17-243">**SingleBox:** Perform the full compilation, with TargetType setting to SingleBox.</span></span></li></ul><p><span data-ttu-id="1bf17-244">Si no se especifica ningún valor para esta propiedad, el servidor determina el modo de compilación óptimo.</span><span class="sxs-lookup"><span data-stu-id="1bf17-244">If you don't specify a value for this property, the server determines the optimal compilation mode.</span></span> </p>| <span data-ttu-id="1bf17-245">No</span><span class="sxs-lookup"><span data-stu-id="1bf17-245">No</span></span> | 

<span data-ttu-id="1bf17-246">Para ver la definición del script, vea [Definición del script SearchLogProcessing.txt](#sample-u-sql-script) .</span><span class="sxs-lookup"><span data-stu-id="1bf17-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for the script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="1bf17-247">Conjuntos de datos de entrada y salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1bf17-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="1bf17-248">Conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="1bf17-248">Input dataset</span></span>
<span data-ttu-id="1bf17-249">En este ejemplo, los datos de entrada residen en Almacén de Azure Data Lake (archivo SearchLog.tsv en la carpeta de datalake/input).</span><span class="sxs-lookup"><span data-stu-id="1bf17-249">In this example, the input data resides in an Azure Data Lake Store (SearchLog.tsv file in the datalake/input folder).</span></span> 

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

### <a name="output-dataset"></a><span data-ttu-id="1bf17-250">Conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="1bf17-250">Output dataset</span></span>
<span data-ttu-id="1bf17-251">En este ejemplo, los datos de salida generados por el script U-SQL se almacenan en Almacén de Azure Data Lake (carpeta datalake/output).</span><span class="sxs-lookup"><span data-stu-id="1bf17-251">In this example, the output data produced by the U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

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

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="1bf17-252">Ejemplo de servicio vinculado de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1bf17-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="1bf17-253">Aquí está la definición del servicio vinculado de Azure Data Lake Store de ejemplo que usan los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="1bf17-253">Here is the definition of the sample Azure Data Lake Store linked service used by the input/output datasets.</span></span> 

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

<span data-ttu-id="1bf17-254">Consulte el artículo sobre cómo [mover datos a Azure Data Lake Store como origen y destino](data-factory-azure-datalake-connector.md) para ver descripciones de las propiedades JSON.</span><span class="sxs-lookup"><span data-stu-id="1bf17-254">See [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="1bf17-255">Script U-SQL</span><span class="sxs-lookup"><span data-stu-id="1bf17-255">Sample U-SQL Script</span></span>

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
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="1bf17-256">ADF pasa dinámicamente los valores de los parámetros **@in** y **@out** del script de U-SQL usando la sección "parameters".</span><span class="sxs-lookup"><span data-stu-id="1bf17-256">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by ADF using the ‘parameters’ section.</span></span> <span data-ttu-id="1bf17-257">Consulte la sección parameters de la definición de canalización.</span><span class="sxs-lookup"><span data-stu-id="1bf17-257">See the ‘parameters’ section in the pipeline definition.</span></span>

<span data-ttu-id="1bf17-258">También puede especificar otras propiedades como degreeOfParallelism y priority en la definición de canalización de los trabajos que se ejecutan en el servicio Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="1bf17-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="1bf17-259">Parámetros dinámicos</span><span class="sxs-lookup"><span data-stu-id="1bf17-259">Dynamic parameters</span></span>
<span data-ttu-id="1bf17-260">En la definición de canalización de ejemplo, se asignan los parámetros in y out con valores codificados de forma rígida.</span><span class="sxs-lookup"><span data-stu-id="1bf17-260">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="1bf17-261">Es posible usar los parámetros dinámicos en su lugar.</span><span class="sxs-lookup"><span data-stu-id="1bf17-261">It is possible to use dynamic parameters instead.</span></span> <span data-ttu-id="1bf17-262">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1bf17-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="1bf17-263">En este caso, los archivos de entrada se siguen tomando de la carpeta /datalake/input; los de salida se generan en la carpeta /datalake/output.</span><span class="sxs-lookup"><span data-stu-id="1bf17-263">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span></span> <span data-ttu-id="1bf17-264">Sin embargo, los nombres de archivo son dinámicos según la hora de inicio del segmento.</span><span class="sxs-lookup"><span data-stu-id="1bf17-264">The file names are dynamic based on the slice start time.</span></span>  

