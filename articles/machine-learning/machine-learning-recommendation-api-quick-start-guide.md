---
title: "Inicio rápido: API Recomendaciones de Azure Machine Learning (ver. 1)| Microsoft Docs"
description: "Recomendaciones de aprendizaje automática de Azure - Guía de inicio rápido"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 0a9d0b6aa1ef734a857ecc16777ba6250909b38d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="quick-start-guide-for-the-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="9a96a-104">Guía de inicio rápido para la API Recomendaciones de Machine Learning (versión 1)</span><span class="sxs-lookup"><span data-stu-id="9a96a-104">Quick start guide for the Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="9a96a-105">Debe empezar a utilizar el servicio [Cognitive Services de la API de Recomendaciones](https://www.microsoft.com/cognitive-services/recommendations-api) en lugar de esta versión.</span><span class="sxs-lookup"><span data-stu-id="9a96a-105">You should start using the [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="9a96a-106">El servicio Cognitive Services de Recomendaciones va a sustituir a este servicio y todas las características nuevas se desarrollarán en esta nueva versión.</span><span class="sxs-lookup"><span data-stu-id="9a96a-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="9a96a-107">Tiene nuevas funcionalidades como compatibilidad con procesamientos por lotes, un explorador de API más eficaz, una interfaz de API más limpia, una experiencia de facturación y suscripción más coherente, etc.</span><span class="sxs-lookup"><span data-stu-id="9a96a-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="9a96a-108">Obtenga más información sobre cómo [migrar al nuevo servicio Cognitive Services](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="9a96a-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="9a96a-109">En este documento se describe cómo incorporar su servicio o aplicación para usar las recomendaciones de Aprendizaje automático de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9a96a-109">This document describes how to onboard your service or application to use Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="9a96a-110">Puede encontrar más detalles sobre Recommendations API en la [galería de Cortana Intelligence](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="9a96a-110">You can find more details on the Recommendations API in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="9a96a-111">Información general</span><span class="sxs-lookup"><span data-stu-id="9a96a-111">General overview</span></span>
<span data-ttu-id="9a96a-112">Para usar las recomendaciones de Aprendizaje automático de Azure, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9a96a-112">To use Azure Machine Learning Recommendations, you need to take the following steps:</span></span>

* <span data-ttu-id="9a96a-113">Crear un modelo: un modelo es un contenedor de los datos de uso, datos del catálogo y el modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-113">Create a model - A model is a container of your usage data, catalog data, and the recommendation model.</span></span>
* <span data-ttu-id="9a96a-114">Importar datos del catálogo: un catálogo contiene información de metadatos sobre los elementos.</span><span class="sxs-lookup"><span data-stu-id="9a96a-114">Import catalog data - A catalog contains metadata information on the items.</span></span> 
* <span data-ttu-id="9a96a-115">Importar datos de uso: los datos de uso se pueden cargar en una de las dos formas siguientes (o ambas):</span><span class="sxs-lookup"><span data-stu-id="9a96a-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="9a96a-116">Mediante la carga de un archivo que contiene los datos de uso.</span><span class="sxs-lookup"><span data-stu-id="9a96a-116">By uploading a file that contains the usage data.</span></span>
  * <span data-ttu-id="9a96a-117">Mediante el envío de eventos de adquisición de datos.</span><span class="sxs-lookup"><span data-stu-id="9a96a-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="9a96a-118">Normalmente, carga un archivo de uso para poder crear un modelo de recomendación inicial (arranque) y usarlo hasta que el sistema reúne suficientes datos con el formato de adquisición de datos.</span><span class="sxs-lookup"><span data-stu-id="9a96a-118">Usually you upload a usage file in order to be able to create an initial recommendation model (bootstrap) and use it until the system gathers enough data by using the data acquisition format.</span></span>
* <span data-ttu-id="9a96a-119">Compilar un modelo de recomendación: se trata de una operación asincrónica en la que el sistema de recomendación toma todos los datos de uso y crea un modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-119">Build a recommendation model - This is an asynchronous operation in which the recommendation system takes all the usage data and creates a recommendation model.</span></span> <span data-ttu-id="9a96a-120">Esta operación puede tardar varios minutos o varias horas, según el tamaño de los datos y los parámetros de configuración de compilación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-120">This operation can take several minutes or several hours depending on the size of the data and the build configuration parameters.</span></span> <span data-ttu-id="9a96a-121">Al desencadenar la compilación, obtendrá un identificador de compilación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-121">When triggering the build, you will get a build ID.</span></span> <span data-ttu-id="9a96a-122">Utilícelo para comprobar cuándo ha finalizado el proceso de compilación antes de empezar a consumir recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="9a96a-122">Use it to check when the build process has ended before starting to consume recommendations.</span></span>
* <span data-ttu-id="9a96a-123">Recomendaciones de uso: obtenga recomendaciones para un elemento específico o una lista de elementos.</span><span class="sxs-lookup"><span data-stu-id="9a96a-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="9a96a-124">Todos los pasos anteriores se realizan a través de la API de recomendaciones de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a96a-124">All the steps above are done through the Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="9a96a-125">Puede descargar una aplicación de ejemplo que implementa cada uno de estos pasos también desde la [galería](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="9a96a-125">You can download a sample application that implements each of these steps from the [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="9a96a-126">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="9a96a-126">Limitations</span></span>
* <span data-ttu-id="9a96a-127">El número máximo de modelos por suscripción es 10.</span><span class="sxs-lookup"><span data-stu-id="9a96a-127">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="9a96a-128">El número máximo de elementos que puede contener un catálogo es 100 000.</span><span class="sxs-lookup"><span data-stu-id="9a96a-128">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="9a96a-129">El número máximo de puntos de uso que se mantienen es ~ 5 000 000.</span><span class="sxs-lookup"><span data-stu-id="9a96a-129">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="9a96a-130">Se eliminarán los más antiguos si se cargan o notifican unos nuevos.</span><span class="sxs-lookup"><span data-stu-id="9a96a-130">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="9a96a-131">El tamaño máximo de datos que puede enviarse en POST (por ejemplo, importar datos de catálogo, importar datos de uso) es de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="9a96a-131">The maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="9a96a-132">El número de transacciones por segundo para una compilación de modelo de recomendación que no está activa es ~ 2TPS.</span><span class="sxs-lookup"><span data-stu-id="9a96a-132">The number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="9a96a-133">Una compilación de modelo de recomendación que está activa puede contener hasta 20TPS.</span><span class="sxs-lookup"><span data-stu-id="9a96a-133">A recommendation model build that is active can hold up to 20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="9a96a-134">Integración</span><span class="sxs-lookup"><span data-stu-id="9a96a-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="9a96a-135">Autenticación</span><span class="sxs-lookup"><span data-stu-id="9a96a-135">Authentication</span></span>
<span data-ttu-id="9a96a-136">Microsoft Azure Marketplace admite métodos de autenticación Básica o OAuth.</span><span class="sxs-lookup"><span data-stu-id="9a96a-136">Microsoft Azure Marketplace supports either the Basic or OAuth authentication method.</span></span> <span data-ttu-id="9a96a-137">Para encontrar las claves de cuenta con facilidad, vaya a las claves del Marketplace en [la configuración de su cuenta](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="9a96a-137">You can easily find the account keys by navigating to the keys in the marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="9a96a-138">Autenticación básica</span><span class="sxs-lookup"><span data-stu-id="9a96a-138">Basic Authentication</span></span>
<span data-ttu-id="9a96a-139">Agregue el encabezado de autorización:</span><span class="sxs-lookup"><span data-stu-id="9a96a-139">Add the Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="9a96a-140">Conviértalo en Base64 (C#)</span><span class="sxs-lookup"><span data-stu-id="9a96a-140">Convert to Base64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="9a96a-141">Conviértalo en Base64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="9a96a-141">Convert to Base64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="9a96a-142">URI de servicio</span><span class="sxs-lookup"><span data-stu-id="9a96a-142">Service URI</span></span>
<span data-ttu-id="9a96a-143">El URI raíz de servicio para cada una de las API de recomendaciones de Aprendizaje automático de Azure se encuentra [aquí](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="9a96a-143">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="9a96a-144">El URI de servicio completo se expresa mediante elementos de la especificación de OData.</span><span class="sxs-lookup"><span data-stu-id="9a96a-144">The full service URI is expressed using elements of the OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="9a96a-145">Versión de API</span><span class="sxs-lookup"><span data-stu-id="9a96a-145">API version</span></span>
<span data-ttu-id="9a96a-146">Cada llamada a la API tendrá al final un parámetro de consulta denominado apiVersion que debe estar establecido en "1.0".</span><span class="sxs-lookup"><span data-stu-id="9a96a-146">Each API call will have, at the end, a query parameter called apiVersion that should be set to "1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="9a96a-147">Los identificadores distinguen mayúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="9a96a-147">IDs are case-sensitive</span></span>
<span data-ttu-id="9a96a-148">Los identificadores devueltos por cualquiera de las API, distinguen mayúsculas de minúsculas y deben usarse como tales cuando se pasan como parámetros en las sucesivas llamadas a API.</span><span class="sxs-lookup"><span data-stu-id="9a96a-148">IDs, returned by any of the APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="9a96a-149">Por ejemplo, los identificadores de modelo y de catálogo distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9a96a-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="9a96a-150">Crear un modelo</span><span class="sxs-lookup"><span data-stu-id="9a96a-150">Create a model</span></span>
<span data-ttu-id="9a96a-151">Creación de una solicitud de "creación de modelo":</span><span class="sxs-lookup"><span data-stu-id="9a96a-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="9a96a-152">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="9a96a-152">HTTP Method</span></span> | <span data-ttu-id="9a96a-153">URI</span><span class="sxs-lookup"><span data-stu-id="9a96a-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-154">POST</span><span class="sxs-lookup"><span data-stu-id="9a96a-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="9a96a-155">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a96a-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="9a96a-156">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="9a96a-156">Parameter Name</span></span> | <span data-ttu-id="9a96a-157">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="9a96a-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-158">modelName</span><span class="sxs-lookup"><span data-stu-id="9a96a-158">modelName</span></span> |<span data-ttu-id="9a96a-159">Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="9a96a-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="9a96a-160">Longitud máxima: 20</span><span class="sxs-lookup"><span data-stu-id="9a96a-160">Max length: 20</span></span> |
| <span data-ttu-id="9a96a-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9a96a-161">apiVersion</span></span> |<span data-ttu-id="9a96a-162">1.0</span><span class="sxs-lookup"><span data-stu-id="9a96a-162">1.0</span></span> |
|  | |
| <span data-ttu-id="9a96a-163">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="9a96a-163">Request Body</span></span> |<span data-ttu-id="9a96a-164">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="9a96a-164">NONE</span></span> |

<span data-ttu-id="9a96a-165">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="9a96a-165">**Response**:</span></span>

<span data-ttu-id="9a96a-166">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9a96a-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="9a96a-167">`feed/entry/content/properties/id`: contiene el id. de modelo.</span><span class="sxs-lookup"><span data-stu-id="9a96a-167">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="9a96a-168">Nota: el identificador de modelo distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9a96a-168">Note that the model ID is case-sensitive.</span></span>

<span data-ttu-id="9a96a-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="9a96a-169">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a><span data-ttu-id="9a96a-170">Importar datos de catálogo</span><span class="sxs-lookup"><span data-stu-id="9a96a-170">Import catalog data</span></span>
<span data-ttu-id="9a96a-171">Si carga varios archivos de catálogo para el mismo modelo con varias llamadas, solo insertaremos los nuevos elementos de catálogo.</span><span class="sxs-lookup"><span data-stu-id="9a96a-171">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="9a96a-172">Los elementos existentes permanecerán con los valores originales.</span><span class="sxs-lookup"><span data-stu-id="9a96a-172">Existing items will remain with the original values.</span></span>

| <span data-ttu-id="9a96a-173">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="9a96a-173">HTTP Method</span></span> | <span data-ttu-id="9a96a-174">URI</span><span class="sxs-lookup"><span data-stu-id="9a96a-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-175">POST</span><span class="sxs-lookup"><span data-stu-id="9a96a-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="9a96a-176">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a96a-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="9a96a-177">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="9a96a-177">Parameter Name</span></span> | <span data-ttu-id="9a96a-178">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="9a96a-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-179">modelId</span><span class="sxs-lookup"><span data-stu-id="9a96a-179">modelId</span></span> |<span data-ttu-id="9a96a-180">Identificador único del modelo (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="9a96a-180">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="9a96a-181">filename</span><span class="sxs-lookup"><span data-stu-id="9a96a-181">filename</span></span> |<span data-ttu-id="9a96a-182">Identificador textual del catálogo.</span><span class="sxs-lookup"><span data-stu-id="9a96a-182">Textual identifier of the catalog.</span></span><br><span data-ttu-id="9a96a-183">Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="9a96a-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="9a96a-184">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="9a96a-184">Max length: 50</span></span> |
| <span data-ttu-id="9a96a-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9a96a-185">apiVersion</span></span> |<span data-ttu-id="9a96a-186">1.0</span><span class="sxs-lookup"><span data-stu-id="9a96a-186">1.0</span></span> |
|  | |
| <span data-ttu-id="9a96a-187">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="9a96a-187">Request Body</span></span> |<span data-ttu-id="9a96a-188">Datos del catálogo.</span><span class="sxs-lookup"><span data-stu-id="9a96a-188">Catalog data.</span></span> <span data-ttu-id="9a96a-189">Formato:</span><span class="sxs-lookup"><span data-stu-id="9a96a-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="9a96a-190">Nombre</span><span class="sxs-lookup"><span data-stu-id="9a96a-190">Name</span></span></th><th><span data-ttu-id="9a96a-191">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="9a96a-191">Mandatory</span></span></th><th><span data-ttu-id="9a96a-192">Tipo</span><span class="sxs-lookup"><span data-stu-id="9a96a-192">Type</span></span></th><th><span data-ttu-id="9a96a-193">Description</span><span class="sxs-lookup"><span data-stu-id="9a96a-193">Description</span></span></th></tr><tr><td><span data-ttu-id="9a96a-194">Id. de elemento</span><span class="sxs-lookup"><span data-stu-id="9a96a-194">Item Id</span></span></td><td><span data-ttu-id="9a96a-195">yes</span><span class="sxs-lookup"><span data-stu-id="9a96a-195">Yes</span></span></td><td><span data-ttu-id="9a96a-196">Alfanumérico, longitud máxima 50</span><span class="sxs-lookup"><span data-stu-id="9a96a-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="9a96a-197">Identificador único de un elemento</span><span class="sxs-lookup"><span data-stu-id="9a96a-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="9a96a-198">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="9a96a-198">Item Name</span></span></td><td><span data-ttu-id="9a96a-199">Sí</span><span class="sxs-lookup"><span data-stu-id="9a96a-199">Yes</span></span></td><td><span data-ttu-id="9a96a-200">Alfanumérico, longitud máxima 255</span><span class="sxs-lookup"><span data-stu-id="9a96a-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="9a96a-201">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="9a96a-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="9a96a-202">Categoría del elemento</span><span class="sxs-lookup"><span data-stu-id="9a96a-202">Item Category</span></span></td><td><span data-ttu-id="9a96a-203">Sí</span><span class="sxs-lookup"><span data-stu-id="9a96a-203">Yes</span></span></td><td><span data-ttu-id="9a96a-204">Alfanumérico, longitud máxima 255</span><span class="sxs-lookup"><span data-stu-id="9a96a-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="9a96a-205">Categoría a la que pertenece este elemento (por ejemplo Libros de cocina, Drama…)</span><span class="sxs-lookup"><span data-stu-id="9a96a-205">Category to which this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="9a96a-206">Descripción</span><span class="sxs-lookup"><span data-stu-id="9a96a-206">Description</span></span></td><td><span data-ttu-id="9a96a-207">No</span><span class="sxs-lookup"><span data-stu-id="9a96a-207">No</span></span></td><td><span data-ttu-id="9a96a-208">Alfanumérico, longitud máxima 4000</span><span class="sxs-lookup"><span data-stu-id="9a96a-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="9a96a-209">Descripción de este elemento</span><span class="sxs-lookup"><span data-stu-id="9a96a-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="9a96a-210">El tamaño máximo de archivo es de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="9a96a-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="9a96a-211">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a96a-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="9a96a-212">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="9a96a-212">**Response**:</span></span>

<span data-ttu-id="9a96a-213">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9a96a-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="9a96a-214">`Feed\entry\content\properties\LineCount` : número de líneas aceptadas.</span><span class="sxs-lookup"><span data-stu-id="9a96a-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="9a96a-215">`Feed\entry\content\properties\ErrorCount` : número de líneas que no se insertaron debido a un error.</span><span class="sxs-lookup"><span data-stu-id="9a96a-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="9a96a-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="9a96a-216">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a><span data-ttu-id="9a96a-217">Importar datos de uso</span><span class="sxs-lookup"><span data-stu-id="9a96a-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="9a96a-218">Carga de un archivo</span><span class="sxs-lookup"><span data-stu-id="9a96a-218">Uploading a file</span></span>
<span data-ttu-id="9a96a-219">En esta sección se muestra cómo cargar datos de uso mediante un archivo.</span><span class="sxs-lookup"><span data-stu-id="9a96a-219">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="9a96a-220">Puede llamar a esta API varias veces con datos de uso.</span><span class="sxs-lookup"><span data-stu-id="9a96a-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="9a96a-221">Todos los datos de uso se guardarán para todas las llamadas.</span><span class="sxs-lookup"><span data-stu-id="9a96a-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="9a96a-222">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="9a96a-222">HTTP Method</span></span> | <span data-ttu-id="9a96a-223">URI</span><span class="sxs-lookup"><span data-stu-id="9a96a-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-224">POST</span><span class="sxs-lookup"><span data-stu-id="9a96a-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="9a96a-225">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a96a-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="9a96a-226">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="9a96a-226">Parameter Name</span></span> | <span data-ttu-id="9a96a-227">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="9a96a-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-228">modelId</span><span class="sxs-lookup"><span data-stu-id="9a96a-228">modelId</span></span> |<span data-ttu-id="9a96a-229">Identificador único del modelo (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="9a96a-229">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="9a96a-230">filename</span><span class="sxs-lookup"><span data-stu-id="9a96a-230">filename</span></span> |<span data-ttu-id="9a96a-231">Identificador textual del catálogo.</span><span class="sxs-lookup"><span data-stu-id="9a96a-231">Textual identifier of the catalog.</span></span><br><span data-ttu-id="9a96a-232">Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="9a96a-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="9a96a-233">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="9a96a-233">Max length: 50</span></span> |
| <span data-ttu-id="9a96a-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9a96a-234">apiVersion</span></span> |<span data-ttu-id="9a96a-235">1.0</span><span class="sxs-lookup"><span data-stu-id="9a96a-235">1.0</span></span> |
|  | |
| <span data-ttu-id="9a96a-236">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="9a96a-236">Request Body</span></span> |<span data-ttu-id="9a96a-237">Datos de uso.</span><span class="sxs-lookup"><span data-stu-id="9a96a-237">Usage data.</span></span> <span data-ttu-id="9a96a-238">Formato:</span><span class="sxs-lookup"><span data-stu-id="9a96a-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="9a96a-239">Nombre</span><span class="sxs-lookup"><span data-stu-id="9a96a-239">Name</span></span></th><th><span data-ttu-id="9a96a-240">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="9a96a-240">Mandatory</span></span></th><th><span data-ttu-id="9a96a-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="9a96a-241">Type</span></span></th><th><span data-ttu-id="9a96a-242">Description</span><span class="sxs-lookup"><span data-stu-id="9a96a-242">Description</span></span></th></tr><tr><td><span data-ttu-id="9a96a-243">Id. de usuario</span><span class="sxs-lookup"><span data-stu-id="9a96a-243">User Id</span></span></td><td><span data-ttu-id="9a96a-244">Sí</span><span class="sxs-lookup"><span data-stu-id="9a96a-244">Yes</span></span></td><td><span data-ttu-id="9a96a-245">Alfanuméricas</span><span class="sxs-lookup"><span data-stu-id="9a96a-245">Alphanumeric</span></span></td><td><span data-ttu-id="9a96a-246">Identificador único de un usuario</span><span class="sxs-lookup"><span data-stu-id="9a96a-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="9a96a-247">Id. de elemento</span><span class="sxs-lookup"><span data-stu-id="9a96a-247">Item Id</span></span></td><td><span data-ttu-id="9a96a-248">yes</span><span class="sxs-lookup"><span data-stu-id="9a96a-248">Yes</span></span></td><td><span data-ttu-id="9a96a-249">Alfanumérico, longitud máxima 50</span><span class="sxs-lookup"><span data-stu-id="9a96a-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="9a96a-250">Identificador único de un elemento</span><span class="sxs-lookup"><span data-stu-id="9a96a-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="9a96a-251">Hora</span><span class="sxs-lookup"><span data-stu-id="9a96a-251">Time</span></span></td><td><span data-ttu-id="9a96a-252">No</span><span class="sxs-lookup"><span data-stu-id="9a96a-252">No</span></span></td><td><span data-ttu-id="9a96a-253">La fecha en este formato: AAAA/MM/DDTHH:MM:SS (por ejemplo, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="9a96a-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="9a96a-254">Hora de los datos</span><span class="sxs-lookup"><span data-stu-id="9a96a-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="9a96a-255">Evento</span><span class="sxs-lookup"><span data-stu-id="9a96a-255">Event</span></span></td><td><span data-ttu-id="9a96a-256">No, si se suministra también se debe colocar la fecha</span><span class="sxs-lookup"><span data-stu-id="9a96a-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="9a96a-257">Uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="9a96a-257">One of the following:</span></span><br><span data-ttu-id="9a96a-258">• Click</span><span class="sxs-lookup"><span data-stu-id="9a96a-258">• Click</span></span><br><span data-ttu-id="9a96a-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="9a96a-259">• RecommendationClick</span></span><br><span data-ttu-id="9a96a-260">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="9a96a-260">•    AddShopCart</span></span><br><span data-ttu-id="9a96a-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="9a96a-261">• RemoveShopCart</span></span><br><span data-ttu-id="9a96a-262">• compra</span><span class="sxs-lookup"><span data-stu-id="9a96a-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="9a96a-263">El tamaño máximo de archivo es de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="9a96a-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="9a96a-264">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a96a-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="9a96a-265">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="9a96a-265">**Response**:</span></span>

<span data-ttu-id="9a96a-266">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9a96a-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="9a96a-267">`Feed\entry\content\properties\LineCount` : número de líneas aceptadas.</span><span class="sxs-lookup"><span data-stu-id="9a96a-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="9a96a-268">`Feed\entry\content\properties\ErrorCount` : número de líneas que no se insertaron debido a un error.</span><span class="sxs-lookup"><span data-stu-id="9a96a-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="9a96a-269">`Feed\entry\content\properties\FileId` : identificador de archivo.</span><span class="sxs-lookup"><span data-stu-id="9a96a-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="9a96a-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="9a96a-270">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a><span data-ttu-id="9a96a-271">Utilizar la adquisición de datos</span><span class="sxs-lookup"><span data-stu-id="9a96a-271">Using data acquisition</span></span>
<span data-ttu-id="9a96a-272">En esta sección se muestra cómo enviar eventos en tiempo real a las recomendaciones de Aprendizaje automático de Azure, normalmente desde su sitio web.</span><span class="sxs-lookup"><span data-stu-id="9a96a-272">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="9a96a-273">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="9a96a-273">HTTP Method</span></span> | <span data-ttu-id="9a96a-274">URI</span><span class="sxs-lookup"><span data-stu-id="9a96a-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-275">POST</span><span class="sxs-lookup"><span data-stu-id="9a96a-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="9a96a-276">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="9a96a-276">Parameter Name</span></span> | <span data-ttu-id="9a96a-277">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="9a96a-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9a96a-278">apiVersion</span></span> |<span data-ttu-id="9a96a-279">1.0</span><span class="sxs-lookup"><span data-stu-id="9a96a-279">1.0</span></span> |
|  | |
| <span data-ttu-id="9a96a-280">Request body</span><span class="sxs-lookup"><span data-stu-id="9a96a-280">Request body</span></span> |<span data-ttu-id="9a96a-281">Entrada de datos de eventos para cada evento que va a enviar.</span><span class="sxs-lookup"><span data-stu-id="9a96a-281">Event data entry for each event you want to send.</span></span> <span data-ttu-id="9a96a-282">Debe enviar para la misma sesión de usuario o explorador el mismo identificador en el campo SessionId.</span><span class="sxs-lookup"><span data-stu-id="9a96a-282">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="9a96a-283">(Vea el ejemplo del cuerpo de evento aparece a continuación).</span><span class="sxs-lookup"><span data-stu-id="9a96a-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="9a96a-284">Ejemplo para evento 'Click':</span><span class="sxs-lookup"><span data-stu-id="9a96a-284">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="9a96a-285">Ejemplo para evento 'RecommendationClick':</span><span class="sxs-lookup"><span data-stu-id="9a96a-285">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="9a96a-286">Ejemplo para evento 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="9a96a-286">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="9a96a-287">Ejemplo para evento 'RemoveShopCart':</span><span class="sxs-lookup"><span data-stu-id="9a96a-287">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="9a96a-288">Ejemplo para el evento “Purchase”:</span><span class="sxs-lookup"><span data-stu-id="9a96a-288">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="9a96a-289">Ejemplo con envío de 2 eventos, 'Click' y 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="9a96a-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="9a96a-290">**Respuesta**: código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9a96a-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="9a96a-291">Compilar un modelo de recomendación</span><span class="sxs-lookup"><span data-stu-id="9a96a-291">Build a recommendation model</span></span>
| <span data-ttu-id="9a96a-292">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="9a96a-292">HTTP Method</span></span> | <span data-ttu-id="9a96a-293">URI</span><span class="sxs-lookup"><span data-stu-id="9a96a-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-294">POST</span><span class="sxs-lookup"><span data-stu-id="9a96a-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="9a96a-295">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a96a-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="9a96a-296">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="9a96a-296">Parameter Name</span></span> | <span data-ttu-id="9a96a-297">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="9a96a-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-298">modelId</span><span class="sxs-lookup"><span data-stu-id="9a96a-298">modelId</span></span> |<span data-ttu-id="9a96a-299">Identificador único del modelo (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="9a96a-299">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="9a96a-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="9a96a-300">userDescription</span></span> |<span data-ttu-id="9a96a-301">Identificador textual del catálogo.</span><span class="sxs-lookup"><span data-stu-id="9a96a-301">Textual identifier of the catalog.</span></span> <span data-ttu-id="9a96a-302">Tenga en cuenta que si usa espacios debe codificarlo en su lugar con un 20 %.</span><span class="sxs-lookup"><span data-stu-id="9a96a-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="9a96a-303">Vea el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="9a96a-303">See example above.</span></span><br><span data-ttu-id="9a96a-304">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="9a96a-304">Max length: 50</span></span> |
| <span data-ttu-id="9a96a-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9a96a-305">apiVersion</span></span> |<span data-ttu-id="9a96a-306">1.0</span><span class="sxs-lookup"><span data-stu-id="9a96a-306">1.0</span></span> |
|  | |
| <span data-ttu-id="9a96a-307">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="9a96a-307">Request Body</span></span> |<span data-ttu-id="9a96a-308">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="9a96a-308">NONE</span></span> |

<span data-ttu-id="9a96a-309">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="9a96a-309">**Response**:</span></span>

<span data-ttu-id="9a96a-310">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9a96a-310">HTTP Status code: 200</span></span>

<span data-ttu-id="9a96a-311">Se trata de una API asincrónica.</span><span class="sxs-lookup"><span data-stu-id="9a96a-311">This is an asynchronous API.</span></span> <span data-ttu-id="9a96a-312">Obtendrá un Id. de compilación como respuesta.</span><span class="sxs-lookup"><span data-stu-id="9a96a-312">You will get a build ID as a response.</span></span> <span data-ttu-id="9a96a-313">Para saber cuándo ha finalizado la compilación, debe llamar a la API "Obtener estados de compilaciones de un modelo" y buscar este id. de compilación en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="9a96a-313">To know when the build has ended, you should call the "Get Builds Status of a Model" API and locate this build ID in the response.</span></span> <span data-ttu-id="9a96a-314">Tenga en cuenta que una compilación puede tardar desde unos minutos hasta varias horas según el tamaño de los datos.</span><span class="sxs-lookup"><span data-stu-id="9a96a-314">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="9a96a-315">No puede usar recomendaciones hasta que no finalice la compilación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-315">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="9a96a-316">Estado de compilación válido:</span><span class="sxs-lookup"><span data-stu-id="9a96a-316">Valid build status:</span></span>

* <span data-ttu-id="9a96a-317">Crear: se creó el modelo.</span><span class="sxs-lookup"><span data-stu-id="9a96a-317">Create – Model was created.</span></span>
* <span data-ttu-id="9a96a-318">Queued: se desencadenó la compilación del modelo y está en la cola.</span><span class="sxs-lookup"><span data-stu-id="9a96a-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="9a96a-319">Building: el modelo se está compilando.</span><span class="sxs-lookup"><span data-stu-id="9a96a-319">Building – Model is being built.</span></span>
* <span data-ttu-id="9a96a-320">Success: la compilación finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="9a96a-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="9a96a-321">Error: la compilación finalizó con un error.</span><span class="sxs-lookup"><span data-stu-id="9a96a-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="9a96a-322">Cancelled: la compilación se canceló.</span><span class="sxs-lookup"><span data-stu-id="9a96a-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="9a96a-323">Cancelling: la compilación se está cancelando.</span><span class="sxs-lookup"><span data-stu-id="9a96a-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="9a96a-324">Tenga en cuenta que el Id. de compilación se puede encontrar en la ruta siguiente: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="9a96a-324">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="9a96a-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="9a96a-325">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="9a96a-326">Obtención del estado de compilación de un modelo</span><span class="sxs-lookup"><span data-stu-id="9a96a-326">Get build status of a model</span></span>
| <span data-ttu-id="9a96a-327">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="9a96a-327">HTTP Method</span></span> | <span data-ttu-id="9a96a-328">URI</span><span class="sxs-lookup"><span data-stu-id="9a96a-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-329">GET</span><span class="sxs-lookup"><span data-stu-id="9a96a-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="9a96a-330">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a96a-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="9a96a-331">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="9a96a-331">Parameter Name</span></span> | <span data-ttu-id="9a96a-332">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="9a96a-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-333">modelId</span><span class="sxs-lookup"><span data-stu-id="9a96a-333">modelId</span></span> |<span data-ttu-id="9a96a-334">Identificador único del modelo (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="9a96a-334">Unique identifier of the model  (case-sensitive)</span></span> |
| <span data-ttu-id="9a96a-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="9a96a-335">onlyLastBuild</span></span> |<span data-ttu-id="9a96a-336">Indica si se devolverá todo el historial de compilaciones del modelo o solo el estado de la compilación más reciente.</span><span class="sxs-lookup"><span data-stu-id="9a96a-336">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="9a96a-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9a96a-337">apiVersion</span></span> |<span data-ttu-id="9a96a-338">1.0</span><span class="sxs-lookup"><span data-stu-id="9a96a-338">1.0</span></span> |

<span data-ttu-id="9a96a-339">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="9a96a-339">**Response**:</span></span>

<span data-ttu-id="9a96a-340">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9a96a-340">HTTP Status code: 200</span></span>

<span data-ttu-id="9a96a-341">La respuesta incluye una entrada por compilación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-341">The response includes one entry per build.</span></span> <span data-ttu-id="9a96a-342">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="9a96a-342">Each entry has the following data:</span></span>

* <span data-ttu-id="9a96a-343">`feed/entry/content/properties/UserName` : nombre del usuario.</span><span class="sxs-lookup"><span data-stu-id="9a96a-343">`feed/entry/content/properties/UserName` – Name of the user.</span></span>
* <span data-ttu-id="9a96a-344">`feed/entry/content/properties/ModelName` : nombre del modelo.</span><span class="sxs-lookup"><span data-stu-id="9a96a-344">`feed/entry/content/properties/ModelName` – Name of the model.</span></span>
* <span data-ttu-id="9a96a-345">`feed/entry/content/properties/ModelId` : identificador único de modelo.</span><span class="sxs-lookup"><span data-stu-id="9a96a-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="9a96a-346">`feed/entry/content/properties/IsDeployed`: si se implementa la compilación (también conocida como</span><span class="sxs-lookup"><span data-stu-id="9a96a-346">`feed/entry/content/properties/IsDeployed` – Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="9a96a-347">compilación activa).</span><span class="sxs-lookup"><span data-stu-id="9a96a-347">active build).</span></span>
* <span data-ttu-id="9a96a-348">`feed/entry/content/properties/BuildId` : identificador único de compilación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="9a96a-349">`feed/entry/content/properties/BuildType` : tipo de la compilación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-349">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="9a96a-350">`feed/entry/content/properties/Status` : estado de la compilación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="9a96a-351">Puede ser uno de los siguientes: Error, Building, Queued, Cancelling, Cancelled o Success.</span><span class="sxs-lookup"><span data-stu-id="9a96a-351">Can be one of the following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="9a96a-352">`feed/entry/content/properties/StatusMessage` : mensaje de estado detallado (se aplica sólo a estados concretos).</span><span class="sxs-lookup"><span data-stu-id="9a96a-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="9a96a-353">`feed/entry/content/properties/Progress` : progreso de la compilación (%).</span><span class="sxs-lookup"><span data-stu-id="9a96a-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="9a96a-354">`feed/entry/content/properties/StartTime` : hora de inicio de la compilación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="9a96a-355">`feed/entry/content/properties/EndTime` : hora de finalización de la compilación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="9a96a-356">`feed/entry/content/properties/ExecutionTime` : duración de la compilación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="9a96a-357">`feed/entry/content/properties/ProgressStep` : detalles sobre la fase actual de una compilación en curso.</span><span class="sxs-lookup"><span data-stu-id="9a96a-357">`feed/entry/content/properties/ProgressStep` – Details about the current stage that a build in progress is in.</span></span>

<span data-ttu-id="9a96a-358">Estado de compilación válido:</span><span class="sxs-lookup"><span data-stu-id="9a96a-358">Valid build status:</span></span>

* <span data-ttu-id="9a96a-359">Creado: se creó la entrada de solicitud de compilación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="9a96a-360">En cola: la solicitud de compilación se ha desencadenado y puesto en cola.</span><span class="sxs-lookup"><span data-stu-id="9a96a-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="9a96a-361">Compilando: la compilación está en curso.</span><span class="sxs-lookup"><span data-stu-id="9a96a-361">Building – Build is in process.</span></span>
* <span data-ttu-id="9a96a-362">Success: la compilación finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="9a96a-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="9a96a-363">Error: la compilación finalizó con un error.</span><span class="sxs-lookup"><span data-stu-id="9a96a-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="9a96a-364">Cancelled: la compilación se canceló.</span><span class="sxs-lookup"><span data-stu-id="9a96a-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="9a96a-365">Cancelling: la compilación se está cancelando.</span><span class="sxs-lookup"><span data-stu-id="9a96a-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="9a96a-366">Valores válidos para el tipo de compilación:</span><span class="sxs-lookup"><span data-stu-id="9a96a-366">Valid values for build type:</span></span>

* <span data-ttu-id="9a96a-367">Rango: compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="9a96a-367">Rank - Rank build.</span></span> <span data-ttu-id="9a96a-368">(Detalles de compilación de rango, consulte el documento "Documentación de API de recomendaciones de aprendizaje automático").</span><span class="sxs-lookup"><span data-stu-id="9a96a-368">(For rank build details, please refer to the "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="9a96a-369">Recomendación: compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="9a96a-370">Fbt: compilación que con frecuencia se compra junta.</span><span class="sxs-lookup"><span data-stu-id="9a96a-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="9a96a-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="9a96a-371">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a><span data-ttu-id="9a96a-372">Obtención de recomendaciones</span><span class="sxs-lookup"><span data-stu-id="9a96a-372">Get recommendations</span></span>
| <span data-ttu-id="9a96a-373">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="9a96a-373">HTTP Method</span></span> | <span data-ttu-id="9a96a-374">URI</span><span class="sxs-lookup"><span data-stu-id="9a96a-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-375">GET</span><span class="sxs-lookup"><span data-stu-id="9a96a-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="9a96a-376">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a96a-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="9a96a-377">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="9a96a-377">Parameter Name</span></span> | <span data-ttu-id="9a96a-378">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="9a96a-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-379">modelId</span><span class="sxs-lookup"><span data-stu-id="9a96a-379">modelId</span></span> |<span data-ttu-id="9a96a-380">Identificador único del modelo (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="9a96a-380">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="9a96a-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="9a96a-381">itemIds</span></span> |<span data-ttu-id="9a96a-382">Lista separada por comas de los elementos para recomendar.</span><span class="sxs-lookup"><span data-stu-id="9a96a-382">Comma-separated list of the items to recommend for.</span></span><br><span data-ttu-id="9a96a-383">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="9a96a-383">Max length: 1024</span></span> |
| <span data-ttu-id="9a96a-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="9a96a-384">numberOfResults</span></span> |<span data-ttu-id="9a96a-385">Número de resultados requeridos</span><span class="sxs-lookup"><span data-stu-id="9a96a-385">Number of required results</span></span> |
| <span data-ttu-id="9a96a-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="9a96a-386">includeMetatadata</span></span> |<span data-ttu-id="9a96a-387">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="9a96a-387">Future use, always false</span></span> |
| <span data-ttu-id="9a96a-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9a96a-388">apiVersion</span></span> |<span data-ttu-id="9a96a-389">1.0</span><span class="sxs-lookup"><span data-stu-id="9a96a-389">1.0</span></span> |

<span data-ttu-id="9a96a-390">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="9a96a-390">**Response:**</span></span>

<span data-ttu-id="9a96a-391">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9a96a-391">HTTP Status code: 200</span></span>

<span data-ttu-id="9a96a-392">La respuesta incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="9a96a-392">The response includes one entry per recommended item.</span></span> <span data-ttu-id="9a96a-393">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="9a96a-393">Each entry has the following data:</span></span>

* <span data-ttu-id="9a96a-394">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="9a96a-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="9a96a-395">`Feed\entry\content\properties\Name`: nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="9a96a-395">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="9a96a-396">`Feed\entry\content\properties\Rating` : clasificación de la recomendación; un número alto significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="9a96a-396">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="9a96a-397">`Feed\entry\content\properties\Reasoning`: razonamiento de la recomendación (por ejemplo, explicaciones de la recomendación).</span><span class="sxs-lookup"><span data-stu-id="9a96a-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="9a96a-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="9a96a-398">OData XML</span></span>

<span data-ttu-id="9a96a-399">En la respuesta de ejemplo a continuación se incluyen 10 elementos recomendados:</span><span class="sxs-lookup"><span data-stu-id="9a96a-399">The example response below includes 10 recommended items:</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a><span data-ttu-id="9a96a-400">Actualización del modelo</span><span class="sxs-lookup"><span data-stu-id="9a96a-400">Update model</span></span>
<span data-ttu-id="9a96a-401">Puede actualizar la descripción del modelo o el identificador de compilación activa.</span><span class="sxs-lookup"><span data-stu-id="9a96a-401">You can update the model description or the active build ID.</span></span>
<span data-ttu-id="9a96a-402">*Id. de compilación activa*: cada compilación para cada modelo tiene un identificador de compilación.</span><span class="sxs-lookup"><span data-stu-id="9a96a-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="9a96a-403">El Id. de compilación activa es la primera compilación correcta de cada nuevo modelo.</span><span class="sxs-lookup"><span data-stu-id="9a96a-403">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="9a96a-404">Una vez que tiene un Id. de compilación activa y realiza compilaciones adicionales para el mismo modelo, necesitará establecerlo explícitamente como el Id. de compilación predeterminado si lo desea.</span><span class="sxs-lookup"><span data-stu-id="9a96a-404">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="9a96a-405">Cuando se usan las recomendaciones, si no especifica el identificador de compilación que desea usar, se utilizará automáticamente el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9a96a-405">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span>

<span data-ttu-id="9a96a-406">Este mecanismo le permite tener un modelo de recomendación en producción para compilar nuevos modelos y probarlos antes de promoverlos a producción.</span><span class="sxs-lookup"><span data-stu-id="9a96a-406">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="9a96a-407">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="9a96a-407">HTTP Method</span></span> | <span data-ttu-id="9a96a-408">URI</span><span class="sxs-lookup"><span data-stu-id="9a96a-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-409">PUT</span><span class="sxs-lookup"><span data-stu-id="9a96a-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="9a96a-410">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a96a-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="9a96a-411">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="9a96a-411">Parameter Name</span></span> | <span data-ttu-id="9a96a-412">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="9a96a-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a96a-413">id</span><span class="sxs-lookup"><span data-stu-id="9a96a-413">id</span></span> |<span data-ttu-id="9a96a-414">Identificador único del modelo (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="9a96a-414">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="9a96a-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9a96a-415">apiVersion</span></span> |<span data-ttu-id="9a96a-416">1.0</span><span class="sxs-lookup"><span data-stu-id="9a96a-416">1.0</span></span> |
|  | |
| <span data-ttu-id="9a96a-417">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="9a96a-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="9a96a-418">Tenga en cuenta que las etiquetas XML Description y ActiveBuildId son opcionales.</span><span class="sxs-lookup"><span data-stu-id="9a96a-418">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="9a96a-419">Si no desea establecer Description o ActiveBuildId, elimine la etiqueta entera.</span><span class="sxs-lookup"><span data-stu-id="9a96a-419">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="9a96a-420">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="9a96a-420">**Response**:</span></span>

<span data-ttu-id="9a96a-421">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9a96a-421">HTTP Status code: 200</span></span>

<span data-ttu-id="9a96a-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="9a96a-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="9a96a-423">Información legal</span><span class="sxs-lookup"><span data-stu-id="9a96a-423">Legal</span></span>
<span data-ttu-id="9a96a-424">Este documento se ofrece "tal cual".</span><span class="sxs-lookup"><span data-stu-id="9a96a-424">This document is provided "as-is".</span></span> <span data-ttu-id="9a96a-425">La información y las opiniones expresadas en este documento, como las direcciones URL y otras referencias a sitios web de Internet, pueden cambiar sin previo aviso.</span><span class="sxs-lookup"><span data-stu-id="9a96a-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="9a96a-426">Algunos ejemplos mencionados se proporcionan únicamente con fines ilustrativos y son ficticios.</span><span class="sxs-lookup"><span data-stu-id="9a96a-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="9a96a-427">No se pretende ninguna asociación o conexión real ni debe deducirse.</span><span class="sxs-lookup"><span data-stu-id="9a96a-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="9a96a-428">Este documento no proporciona ningún derecho legal a la propiedad intelectual de ningún producto de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9a96a-428">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="9a96a-429">Puede copiar y usar este documento con fines internos y de referencia.</span><span class="sxs-lookup"><span data-stu-id="9a96a-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="9a96a-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9a96a-430">© 2014 Microsoft.</span></span> <span data-ttu-id="9a96a-431">Todos los derechos reservados.</span><span class="sxs-lookup"><span data-stu-id="9a96a-431">All rights reserved.</span></span> 

