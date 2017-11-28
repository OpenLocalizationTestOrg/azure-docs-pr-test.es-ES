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
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="3241e-104">Guía de inicio rápido de hello (versión 1) de la API de recomendaciones de aprendizaje de máquina</span><span class="sxs-lookup"><span data-stu-id="3241e-104">Quick start guide for hello Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="3241e-105">Debería empezar a utilizar hello [recomendaciones API cognitivos servicio](https://www.microsoft.com/cognitive-services/recommendations-api) en lugar de esta versión.</span><span class="sxs-lookup"><span data-stu-id="3241e-105">You should start using hello [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="3241e-106">Hola recomendaciones cognitivos servicio va a sustituir este servicio y todas las características nuevas de Hola se van a desarrollar no existe.</span><span class="sxs-lookup"><span data-stu-id="3241e-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="3241e-107">Tiene nuevas funcionalidades como compatibilidad con procesamientos por lotes, un explorador de API más eficaz, una interfaz de API más limpia, una experiencia de facturación y suscripción más coherente, etc.</span><span class="sxs-lookup"><span data-stu-id="3241e-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="3241e-108">Obtenga más información sobre [toohello de migración nuevo servicio cognitivos](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="3241e-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="3241e-109">Este documento se describe cómo tooonboard su servicio o aplicación toouse recomendaciones de aprendizaje de máquina de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3241e-109">This document describes how tooonboard your service or application toouse Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="3241e-110">Puede encontrar más detalles en hello API recomendaciones en hello [Cortana Intelligence galería](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="3241e-110">You can find more details on hello Recommendations API in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="3241e-111">Información general</span><span class="sxs-lookup"><span data-stu-id="3241e-111">General overview</span></span>
<span data-ttu-id="3241e-112">toouse recomendaciones de aprendizaje de máquina de Azure, necesita hello tootake pasos:</span><span class="sxs-lookup"><span data-stu-id="3241e-112">toouse Azure Machine Learning Recommendations, you need tootake hello following steps:</span></span>

* <span data-ttu-id="3241e-113">Crear un modelo: un modelo es un contenedor de datos de uso, datos del catálogo y del modelo de recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-113">Create a model - A model is a container of your usage data, catalog data, and hello recommendation model.</span></span>
* <span data-ttu-id="3241e-114">Importar datos de catálogo: un catálogo contienen información de metadatos en los elementos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-114">Import catalog data - A catalog contains metadata information on hello items.</span></span> 
* <span data-ttu-id="3241e-115">Importar datos de uso: los datos de uso se pueden cargar en una de las dos formas siguientes (o ambas):</span><span class="sxs-lookup"><span data-stu-id="3241e-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="3241e-116">Si carga un archivo que contiene datos de uso de saludo.</span><span class="sxs-lookup"><span data-stu-id="3241e-116">By uploading a file that contains hello usage data.</span></span>
  * <span data-ttu-id="3241e-117">Mediante el envío de eventos de adquisición de datos.</span><span class="sxs-lookup"><span data-stu-id="3241e-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="3241e-118">Normalmente carga un archivo de uso en orden toobe puede toocreate un modelo de recomendación inicial (arranque) y usarlo hasta que el sistema de hello recopila suficientes datos con formato de adquisición de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-118">Usually you upload a usage file in order toobe able toocreate an initial recommendation model (bootstrap) and use it until hello system gathers enough data by using hello data acquisition format.</span></span>
* <span data-ttu-id="3241e-119">Crear un modelo de recomendación: se trata de una operación asincrónica en qué Hola sistema recomendación toma todos los datos de uso de Hola y crea un modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="3241e-119">Build a recommendation model - This is an asynchronous operation in which hello recommendation system takes all hello usage data and creates a recommendation model.</span></span> <span data-ttu-id="3241e-120">Esta operación puede tardar varios minutos o varias horas, según Hola parámetros de configuración de compilación de tamaño de datos de Hola y Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-120">This operation can take several minutes or several hours depending on hello size of hello data and hello build configuration parameters.</span></span> <span data-ttu-id="3241e-121">Cuando se desencadenan compilación hello, obtendrá un identificador de compilación.</span><span class="sxs-lookup"><span data-stu-id="3241e-121">When triggering hello build, you will get a build ID.</span></span> <span data-ttu-id="3241e-122">Usar toocheck al proceso de compilación de hello ha finalizado antes de iniciar tooconsume recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="3241e-122">Use it toocheck when hello build process has ended before starting tooconsume recommendations.</span></span>
* <span data-ttu-id="3241e-123">Recomendaciones de uso: obtenga recomendaciones para un elemento específico o una lista de elementos.</span><span class="sxs-lookup"><span data-stu-id="3241e-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="3241e-124">Todos los pasos de hello anteriores se realizan a través de hello API de recomendaciones de aprendizaje de máquina de Azure.</span><span class="sxs-lookup"><span data-stu-id="3241e-124">All hello steps above are done through hello Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="3241e-125">Puede descargar una aplicación de ejemplo que implementa cada uno de estos pasos de hello [así la galería.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="3241e-125">You can download a sample application that implements each of these steps from hello [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="3241e-126">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="3241e-126">Limitations</span></span>
* <span data-ttu-id="3241e-127">número máximo de Hola de modelos por suscripción es 10.</span><span class="sxs-lookup"><span data-stu-id="3241e-127">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="3241e-128">número máximo de Hola de elementos que puede contener un catálogo es 100.000.</span><span class="sxs-lookup"><span data-stu-id="3241e-128">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="3241e-129">número máximo de Hola de puntos de uso que se mantienen es ~ 5 000 000.</span><span class="sxs-lookup"><span data-stu-id="3241e-129">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="3241e-130">Hola más antigua se eliminará si nuevos se cargan o se notificarán.</span><span class="sxs-lookup"><span data-stu-id="3241e-130">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="3241e-131">tamaño máximo de Hola de datos que se pueden enviar en POST (por ejemplo, importar datos del catálogo, importar datos de uso) es 200MB.</span><span class="sxs-lookup"><span data-stu-id="3241e-131">hello maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="3241e-132">Hello número de transacciones por segundo para una compilación de modelo de recomendación que no está activa es ~ 2TPS.</span><span class="sxs-lookup"><span data-stu-id="3241e-132">hello number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="3241e-133">Una compilación de modelo de recomendación que está activa puede contener una too20TPS.</span><span class="sxs-lookup"><span data-stu-id="3241e-133">A recommendation model build that is active can hold up too20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="3241e-134">Integración</span><span class="sxs-lookup"><span data-stu-id="3241e-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="3241e-135">Autenticación</span><span class="sxs-lookup"><span data-stu-id="3241e-135">Authentication</span></span>
<span data-ttu-id="3241e-136">Microsoft Azure Marketplace es compatible con cualquier método de autenticación básica o OAuth Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-136">Microsoft Azure Marketplace supports either hello Basic or OAuth authentication method.</span></span> <span data-ttu-id="3241e-137">Puedes buscar fácilmente Hola claves de cuenta desplazándose toohello claves en marketplace de hello en [la configuración de la cuenta](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="3241e-137">You can easily find hello account keys by navigating toohello keys in hello marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="3241e-138">Autenticación básica</span><span class="sxs-lookup"><span data-stu-id="3241e-138">Basic Authentication</span></span>
<span data-ttu-id="3241e-139">Agregar encabezado de autorización de hello:</span><span class="sxs-lookup"><span data-stu-id="3241e-139">Add hello Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="3241e-140">Convertir tooBase64 (C#)</span><span class="sxs-lookup"><span data-stu-id="3241e-140">Convert tooBase64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="3241e-141">Convertir tooBase64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="3241e-141">Convert tooBase64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="3241e-142">URI de servicio</span><span class="sxs-lookup"><span data-stu-id="3241e-142">Service URI</span></span>
<span data-ttu-id="3241e-143">Hola URI raíz del servicio para las API de Azure Machine Learning recomendaciones hello es [aquí.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="3241e-143">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="3241e-144">URI del servicio completo Hola se expresa mediante elementos de especificación de OData de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-144">hello full service URI is expressed using elements of hello OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="3241e-145">Versión de API</span><span class="sxs-lookup"><span data-stu-id="3241e-145">API version</span></span>
<span data-ttu-id="3241e-146">Cada llamada a la API tendrá, al final de hello, un parámetro de consulta denominado valor apiVersion que se debe establecer demasiado "1.0".</span><span class="sxs-lookup"><span data-stu-id="3241e-146">Each API call will have, at hello end, a query parameter called apiVersion that should be set too"1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="3241e-147">Los identificadores distinguen mayúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="3241e-147">IDs are case-sensitive</span></span>
<span data-ttu-id="3241e-148">Identificadores, devueltos por cualquiera de hello API, distinguen mayúsculas de minúsculas y deben usarse como tales cuando se pasan como parámetros en llamadas posteriores a la API.</span><span class="sxs-lookup"><span data-stu-id="3241e-148">IDs, returned by any of hello APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="3241e-149">Por ejemplo, los identificadores de modelo y de catálogo distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3241e-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="3241e-150">Crear un modelo</span><span class="sxs-lookup"><span data-stu-id="3241e-150">Create a model</span></span>
<span data-ttu-id="3241e-151">Creación de una solicitud de "creación de modelo":</span><span class="sxs-lookup"><span data-stu-id="3241e-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="3241e-152">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="3241e-152">HTTP Method</span></span> | <span data-ttu-id="3241e-153">URI</span><span class="sxs-lookup"><span data-stu-id="3241e-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-154">POST</span><span class="sxs-lookup"><span data-stu-id="3241e-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3241e-155">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3241e-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3241e-156">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="3241e-156">Parameter Name</span></span> | <span data-ttu-id="3241e-157">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="3241e-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-158">modelName</span><span class="sxs-lookup"><span data-stu-id="3241e-158">modelName</span></span> |<span data-ttu-id="3241e-159">Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="3241e-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="3241e-160">Longitud máxima: 20</span><span class="sxs-lookup"><span data-stu-id="3241e-160">Max length: 20</span></span> |
| <span data-ttu-id="3241e-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3241e-161">apiVersion</span></span> |<span data-ttu-id="3241e-162">1.0</span><span class="sxs-lookup"><span data-stu-id="3241e-162">1.0</span></span> |
|  | |
| <span data-ttu-id="3241e-163">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="3241e-163">Request Body</span></span> |<span data-ttu-id="3241e-164">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="3241e-164">NONE</span></span> |

<span data-ttu-id="3241e-165">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="3241e-165">**Response**:</span></span>

<span data-ttu-id="3241e-166">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3241e-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="3241e-167">`feed/entry/content/properties/id`-Contiene el identificador del modelo Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-167">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="3241e-168">Tenga en cuenta que el Id. de modelo de hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3241e-168">Note that hello model ID is case-sensitive.</span></span>

<span data-ttu-id="3241e-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="3241e-169">OData XML</span></span>

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


### <a name="import-catalog-data"></a><span data-ttu-id="3241e-170">Importar datos de catálogo</span><span class="sxs-lookup"><span data-stu-id="3241e-170">Import catalog data</span></span>
<span data-ttu-id="3241e-171">Si va a cargar varias catálogo archivos toohello mismo modelo con varias llamadas, insertamos solo Hola nuevos elementos de catálogo.</span><span class="sxs-lookup"><span data-stu-id="3241e-171">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="3241e-172">Los elementos existentes permanecerán con valores originales de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-172">Existing items will remain with hello original values.</span></span>

| <span data-ttu-id="3241e-173">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="3241e-173">HTTP Method</span></span> | <span data-ttu-id="3241e-174">URI</span><span class="sxs-lookup"><span data-stu-id="3241e-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-175">POST</span><span class="sxs-lookup"><span data-stu-id="3241e-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3241e-176">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3241e-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3241e-177">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="3241e-177">Parameter Name</span></span> | <span data-ttu-id="3241e-178">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="3241e-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-179">modelId</span><span class="sxs-lookup"><span data-stu-id="3241e-179">modelId</span></span> |<span data-ttu-id="3241e-180">Identificador único del modelo de hello (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="3241e-180">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="3241e-181">filename</span><span class="sxs-lookup"><span data-stu-id="3241e-181">filename</span></span> |<span data-ttu-id="3241e-182">Identificador textual del catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-182">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="3241e-183">Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="3241e-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="3241e-184">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="3241e-184">Max length: 50</span></span> |
| <span data-ttu-id="3241e-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3241e-185">apiVersion</span></span> |<span data-ttu-id="3241e-186">1.0</span><span class="sxs-lookup"><span data-stu-id="3241e-186">1.0</span></span> |
|  | |
| <span data-ttu-id="3241e-187">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="3241e-187">Request Body</span></span> |<span data-ttu-id="3241e-188">Datos del catálogo.</span><span class="sxs-lookup"><span data-stu-id="3241e-188">Catalog data.</span></span> <span data-ttu-id="3241e-189">Formato:</span><span class="sxs-lookup"><span data-stu-id="3241e-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="3241e-190">Nombre</span><span class="sxs-lookup"><span data-stu-id="3241e-190">Name</span></span></th><th><span data-ttu-id="3241e-191">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="3241e-191">Mandatory</span></span></th><th><span data-ttu-id="3241e-192">Tipo</span><span class="sxs-lookup"><span data-stu-id="3241e-192">Type</span></span></th><th><span data-ttu-id="3241e-193">Description</span><span class="sxs-lookup"><span data-stu-id="3241e-193">Description</span></span></th></tr><tr><td><span data-ttu-id="3241e-194">Id. de elemento</span><span class="sxs-lookup"><span data-stu-id="3241e-194">Item Id</span></span></td><td><span data-ttu-id="3241e-195">yes</span><span class="sxs-lookup"><span data-stu-id="3241e-195">Yes</span></span></td><td><span data-ttu-id="3241e-196">Alfanumérico, longitud máxima 50</span><span class="sxs-lookup"><span data-stu-id="3241e-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="3241e-197">Identificador único de un elemento</span><span class="sxs-lookup"><span data-stu-id="3241e-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="3241e-198">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="3241e-198">Item Name</span></span></td><td><span data-ttu-id="3241e-199">Sí</span><span class="sxs-lookup"><span data-stu-id="3241e-199">Yes</span></span></td><td><span data-ttu-id="3241e-200">Alfanumérico, longitud máxima 255</span><span class="sxs-lookup"><span data-stu-id="3241e-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="3241e-201">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="3241e-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="3241e-202">Categoría del elemento</span><span class="sxs-lookup"><span data-stu-id="3241e-202">Item Category</span></span></td><td><span data-ttu-id="3241e-203">Sí</span><span class="sxs-lookup"><span data-stu-id="3241e-203">Yes</span></span></td><td><span data-ttu-id="3241e-204">Alfanumérico, longitud máxima 255</span><span class="sxs-lookup"><span data-stu-id="3241e-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="3241e-205">Toowhich categoría que este elemento pertenece (por ejemplo, libros de cocina, series...)</span><span class="sxs-lookup"><span data-stu-id="3241e-205">Category toowhich this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="3241e-206">Descripción</span><span class="sxs-lookup"><span data-stu-id="3241e-206">Description</span></span></td><td><span data-ttu-id="3241e-207">No</span><span class="sxs-lookup"><span data-stu-id="3241e-207">No</span></span></td><td><span data-ttu-id="3241e-208">Alfanumérico, longitud máxima 4000</span><span class="sxs-lookup"><span data-stu-id="3241e-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="3241e-209">Descripción de este elemento</span><span class="sxs-lookup"><span data-stu-id="3241e-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="3241e-210">El tamaño máximo de archivo es de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="3241e-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="3241e-211">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3241e-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="3241e-212">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="3241e-212">**Response**:</span></span>

<span data-ttu-id="3241e-213">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3241e-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="3241e-214">`Feed\entry\content\properties\LineCount` : número de líneas aceptadas.</span><span class="sxs-lookup"><span data-stu-id="3241e-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="3241e-215">`Feed\entry\content\properties\ErrorCount`-Número de líneas que no se insertaron debido a error de tooan.</span><span class="sxs-lookup"><span data-stu-id="3241e-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="3241e-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="3241e-216">OData XML</span></span>

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


### <a name="import-usage-data"></a><span data-ttu-id="3241e-217">Importar datos de uso</span><span class="sxs-lookup"><span data-stu-id="3241e-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="3241e-218">Carga de un archivo</span><span class="sxs-lookup"><span data-stu-id="3241e-218">Uploading a file</span></span>
<span data-ttu-id="3241e-219">Esta sección se muestra cómo los datos de uso de tooupload mediante un archivo.</span><span class="sxs-lookup"><span data-stu-id="3241e-219">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="3241e-220">Puede llamar a esta API varias veces con datos de uso.</span><span class="sxs-lookup"><span data-stu-id="3241e-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="3241e-221">Todos los datos de uso se guardarán para todas las llamadas.</span><span class="sxs-lookup"><span data-stu-id="3241e-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="3241e-222">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="3241e-222">HTTP Method</span></span> | <span data-ttu-id="3241e-223">URI</span><span class="sxs-lookup"><span data-stu-id="3241e-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-224">POST</span><span class="sxs-lookup"><span data-stu-id="3241e-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3241e-225">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3241e-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3241e-226">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="3241e-226">Parameter Name</span></span> | <span data-ttu-id="3241e-227">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="3241e-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-228">modelId</span><span class="sxs-lookup"><span data-stu-id="3241e-228">modelId</span></span> |<span data-ttu-id="3241e-229">Identificador único del modelo de hello (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="3241e-229">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="3241e-230">filename</span><span class="sxs-lookup"><span data-stu-id="3241e-230">filename</span></span> |<span data-ttu-id="3241e-231">Identificador textual del catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-231">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="3241e-232">Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="3241e-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="3241e-233">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="3241e-233">Max length: 50</span></span> |
| <span data-ttu-id="3241e-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3241e-234">apiVersion</span></span> |<span data-ttu-id="3241e-235">1.0</span><span class="sxs-lookup"><span data-stu-id="3241e-235">1.0</span></span> |
|  | |
| <span data-ttu-id="3241e-236">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="3241e-236">Request Body</span></span> |<span data-ttu-id="3241e-237">Datos de uso.</span><span class="sxs-lookup"><span data-stu-id="3241e-237">Usage data.</span></span> <span data-ttu-id="3241e-238">Formato:</span><span class="sxs-lookup"><span data-stu-id="3241e-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="3241e-239">Nombre</span><span class="sxs-lookup"><span data-stu-id="3241e-239">Name</span></span></th><th><span data-ttu-id="3241e-240">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="3241e-240">Mandatory</span></span></th><th><span data-ttu-id="3241e-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="3241e-241">Type</span></span></th><th><span data-ttu-id="3241e-242">Description</span><span class="sxs-lookup"><span data-stu-id="3241e-242">Description</span></span></th></tr><tr><td><span data-ttu-id="3241e-243">Id. de usuario</span><span class="sxs-lookup"><span data-stu-id="3241e-243">User Id</span></span></td><td><span data-ttu-id="3241e-244">Sí</span><span class="sxs-lookup"><span data-stu-id="3241e-244">Yes</span></span></td><td><span data-ttu-id="3241e-245">Alfanuméricas</span><span class="sxs-lookup"><span data-stu-id="3241e-245">Alphanumeric</span></span></td><td><span data-ttu-id="3241e-246">Identificador único de un usuario</span><span class="sxs-lookup"><span data-stu-id="3241e-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="3241e-247">Id. de elemento</span><span class="sxs-lookup"><span data-stu-id="3241e-247">Item Id</span></span></td><td><span data-ttu-id="3241e-248">yes</span><span class="sxs-lookup"><span data-stu-id="3241e-248">Yes</span></span></td><td><span data-ttu-id="3241e-249">Alfanumérico, longitud máxima 50</span><span class="sxs-lookup"><span data-stu-id="3241e-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="3241e-250">Identificador único de un elemento</span><span class="sxs-lookup"><span data-stu-id="3241e-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="3241e-251">Hora</span><span class="sxs-lookup"><span data-stu-id="3241e-251">Time</span></span></td><td><span data-ttu-id="3241e-252">No</span><span class="sxs-lookup"><span data-stu-id="3241e-252">No</span></span></td><td><span data-ttu-id="3241e-253">La fecha en este formato: AAAA/MM/DDTHH:MM:SS (por ejemplo, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="3241e-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="3241e-254">Hora de los datos</span><span class="sxs-lookup"><span data-stu-id="3241e-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="3241e-255">Evento</span><span class="sxs-lookup"><span data-stu-id="3241e-255">Event</span></span></td><td><span data-ttu-id="3241e-256">No, si se suministra también se debe colocar la fecha</span><span class="sxs-lookup"><span data-stu-id="3241e-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="3241e-257">Uno de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="3241e-257">One of hello following:</span></span><br><span data-ttu-id="3241e-258">• Click</span><span class="sxs-lookup"><span data-stu-id="3241e-258">• Click</span></span><br><span data-ttu-id="3241e-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="3241e-259">• RecommendationClick</span></span><br><span data-ttu-id="3241e-260">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="3241e-260">•    AddShopCart</span></span><br><span data-ttu-id="3241e-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="3241e-261">• RemoveShopCart</span></span><br><span data-ttu-id="3241e-262">• compra</span><span class="sxs-lookup"><span data-stu-id="3241e-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="3241e-263">El tamaño máximo de archivo es de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="3241e-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="3241e-264">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3241e-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="3241e-265">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="3241e-265">**Response**:</span></span>

<span data-ttu-id="3241e-266">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3241e-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="3241e-267">`Feed\entry\content\properties\LineCount` : número de líneas aceptadas.</span><span class="sxs-lookup"><span data-stu-id="3241e-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="3241e-268">`Feed\entry\content\properties\ErrorCount`-Número de líneas que no se insertaron debido a error de tooan.</span><span class="sxs-lookup"><span data-stu-id="3241e-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="3241e-269">`Feed\entry\content\properties\FileId` : identificador de archivo.</span><span class="sxs-lookup"><span data-stu-id="3241e-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="3241e-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="3241e-270">OData XML</span></span>

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


#### <a name="using-data-acquisition"></a><span data-ttu-id="3241e-271">Utilizar la adquisición de datos</span><span class="sxs-lookup"><span data-stu-id="3241e-271">Using data acquisition</span></span>
<span data-ttu-id="3241e-272">Esta sección muestra cómo toosend eventos real hora de recomendaciones de aprendizaje de máquina tooAzure, normalmente desde su sitio Web.</span><span class="sxs-lookup"><span data-stu-id="3241e-272">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="3241e-273">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="3241e-273">HTTP Method</span></span> | <span data-ttu-id="3241e-274">URI</span><span class="sxs-lookup"><span data-stu-id="3241e-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-275">POST</span><span class="sxs-lookup"><span data-stu-id="3241e-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3241e-276">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="3241e-276">Parameter Name</span></span> | <span data-ttu-id="3241e-277">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="3241e-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3241e-278">apiVersion</span></span> |<span data-ttu-id="3241e-279">1.0</span><span class="sxs-lookup"><span data-stu-id="3241e-279">1.0</span></span> |
|  | |
| <span data-ttu-id="3241e-280">Request body</span><span class="sxs-lookup"><span data-stu-id="3241e-280">Request body</span></span> |<span data-ttu-id="3241e-281">Entrada de datos de evento para cada evento que desee toosend.</span><span class="sxs-lookup"><span data-stu-id="3241e-281">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="3241e-282">Debe enviar para la misma sesión de usuario o el Examinador de Hola Hola mismo identificador en el campo de SessionId Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-282">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="3241e-283">(Vea el ejemplo del cuerpo de evento aparece a continuación).</span><span class="sxs-lookup"><span data-stu-id="3241e-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="3241e-284">Ejemplo para evento 'Click':</span><span class="sxs-lookup"><span data-stu-id="3241e-284">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="3241e-285">Ejemplo para evento 'RecommendationClick':</span><span class="sxs-lookup"><span data-stu-id="3241e-285">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="3241e-286">Ejemplo para evento 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="3241e-286">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="3241e-287">Ejemplo para evento 'RemoveShopCart':</span><span class="sxs-lookup"><span data-stu-id="3241e-287">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="3241e-288">Ejemplo para el evento “Purchase”:</span><span class="sxs-lookup"><span data-stu-id="3241e-288">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="3241e-289">Ejemplo con envío de 2 eventos, 'Click' y 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="3241e-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="3241e-290">**Respuesta**: código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3241e-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="3241e-291">Compilar un modelo de recomendación</span><span class="sxs-lookup"><span data-stu-id="3241e-291">Build a recommendation model</span></span>
| <span data-ttu-id="3241e-292">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="3241e-292">HTTP Method</span></span> | <span data-ttu-id="3241e-293">URI</span><span class="sxs-lookup"><span data-stu-id="3241e-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-294">POST</span><span class="sxs-lookup"><span data-stu-id="3241e-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3241e-295">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3241e-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3241e-296">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="3241e-296">Parameter Name</span></span> | <span data-ttu-id="3241e-297">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="3241e-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-298">modelId</span><span class="sxs-lookup"><span data-stu-id="3241e-298">modelId</span></span> |<span data-ttu-id="3241e-299">Identificador único del modelo de hello (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="3241e-299">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="3241e-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="3241e-300">userDescription</span></span> |<span data-ttu-id="3241e-301">Identificador textual del catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-301">Textual identifier of hello catalog.</span></span> <span data-ttu-id="3241e-302">Tenga en cuenta que si usa espacios debe codificarlo en su lugar con un 20 %.</span><span class="sxs-lookup"><span data-stu-id="3241e-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="3241e-303">Vea el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="3241e-303">See example above.</span></span><br><span data-ttu-id="3241e-304">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="3241e-304">Max length: 50</span></span> |
| <span data-ttu-id="3241e-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3241e-305">apiVersion</span></span> |<span data-ttu-id="3241e-306">1.0</span><span class="sxs-lookup"><span data-stu-id="3241e-306">1.0</span></span> |
|  | |
| <span data-ttu-id="3241e-307">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="3241e-307">Request Body</span></span> |<span data-ttu-id="3241e-308">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="3241e-308">NONE</span></span> |

<span data-ttu-id="3241e-309">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="3241e-309">**Response**:</span></span>

<span data-ttu-id="3241e-310">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3241e-310">HTTP Status code: 200</span></span>

<span data-ttu-id="3241e-311">Se trata de una API asincrónica.</span><span class="sxs-lookup"><span data-stu-id="3241e-311">This is an asynchronous API.</span></span> <span data-ttu-id="3241e-312">Obtendrá un Id. de compilación como respuesta.</span><span class="sxs-lookup"><span data-stu-id="3241e-312">You will get a build ID as a response.</span></span> <span data-ttu-id="3241e-313">tooknow cuando ha finalizado la generación de hello, debe llamar a la API de "Obtener compilaciones estado de un modelo de" hello y busque este Id. de compilación en la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-313">tooknow when hello build has ended, you should call hello "Get Builds Status of a Model" API and locate this build ID in hello response.</span></span> <span data-ttu-id="3241e-314">Tenga en cuenta que una compilación puede tardar desde toohours minutos según el tamaño de Hola de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-314">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="3241e-315">No se puede consumir recomendaciones hasta Hola crear extremos.</span><span class="sxs-lookup"><span data-stu-id="3241e-315">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="3241e-316">Estado de compilación válido:</span><span class="sxs-lookup"><span data-stu-id="3241e-316">Valid build status:</span></span>

* <span data-ttu-id="3241e-317">Crear: se creó el modelo.</span><span class="sxs-lookup"><span data-stu-id="3241e-317">Create – Model was created.</span></span>
* <span data-ttu-id="3241e-318">Queued: se desencadenó la compilación del modelo y está en la cola.</span><span class="sxs-lookup"><span data-stu-id="3241e-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="3241e-319">Building: el modelo se está compilando.</span><span class="sxs-lookup"><span data-stu-id="3241e-319">Building – Model is being built.</span></span>
* <span data-ttu-id="3241e-320">Success: la compilación finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="3241e-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="3241e-321">Error: la compilación finalizó con un error.</span><span class="sxs-lookup"><span data-stu-id="3241e-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="3241e-322">Cancelled: la compilación se canceló.</span><span class="sxs-lookup"><span data-stu-id="3241e-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="3241e-323">Cancelling: la compilación se está cancelando.</span><span class="sxs-lookup"><span data-stu-id="3241e-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="3241e-324">Tenga en cuenta esa compilación Hola que identificador puede encontrarse en hello siguiendo la ruta de acceso:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="3241e-324">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="3241e-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="3241e-325">OData XML</span></span>

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

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="3241e-326">Obtención del estado de compilación de un modelo</span><span class="sxs-lookup"><span data-stu-id="3241e-326">Get build status of a model</span></span>
| <span data-ttu-id="3241e-327">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="3241e-327">HTTP Method</span></span> | <span data-ttu-id="3241e-328">URI</span><span class="sxs-lookup"><span data-stu-id="3241e-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-329">GET</span><span class="sxs-lookup"><span data-stu-id="3241e-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3241e-330">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3241e-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="3241e-331">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="3241e-331">Parameter Name</span></span> | <span data-ttu-id="3241e-332">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="3241e-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-333">modelId</span><span class="sxs-lookup"><span data-stu-id="3241e-333">modelId</span></span> |<span data-ttu-id="3241e-334">Identificador único del modelo de hello (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="3241e-334">Unique identifier of hello model  (case-sensitive)</span></span> |
| <span data-ttu-id="3241e-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="3241e-335">onlyLastBuild</span></span> |<span data-ttu-id="3241e-336">Indica si tooreturn Hola a todos crear historial de modelo de Hola o solo de estado de Hola de compilación más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-336">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="3241e-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3241e-337">apiVersion</span></span> |<span data-ttu-id="3241e-338">1.0</span><span class="sxs-lookup"><span data-stu-id="3241e-338">1.0</span></span> |

<span data-ttu-id="3241e-339">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="3241e-339">**Response**:</span></span>

<span data-ttu-id="3241e-340">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3241e-340">HTTP Status code: 200</span></span>

<span data-ttu-id="3241e-341">respuesta de Hello incluye una entrada por cada compilación.</span><span class="sxs-lookup"><span data-stu-id="3241e-341">hello response includes one entry per build.</span></span> <span data-ttu-id="3241e-342">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3241e-342">Each entry has hello following data:</span></span>

* <span data-ttu-id="3241e-343">`feed/entry/content/properties/UserName`: Nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-343">`feed/entry/content/properties/UserName` – Name of hello user.</span></span>
* <span data-ttu-id="3241e-344">`feed/entry/content/properties/ModelName`: Nombre del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-344">`feed/entry/content/properties/ModelName` – Name of hello model.</span></span>
* <span data-ttu-id="3241e-345">`feed/entry/content/properties/ModelId` : identificador único de modelo.</span><span class="sxs-lookup"><span data-stu-id="3241e-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="3241e-346">`feed/entry/content/properties/IsDeployed`: Si se implementa compilación hello (conocido como)</span><span class="sxs-lookup"><span data-stu-id="3241e-346">`feed/entry/content/properties/IsDeployed` – Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="3241e-347">compilación activa).</span><span class="sxs-lookup"><span data-stu-id="3241e-347">active build).</span></span>
* <span data-ttu-id="3241e-348">`feed/entry/content/properties/BuildId` : identificador único de compilación.</span><span class="sxs-lookup"><span data-stu-id="3241e-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="3241e-349">`feed/entry/content/properties/BuildType`-Tipo de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-349">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="3241e-350">`feed/entry/content/properties/Status` : estado de la compilación.</span><span class="sxs-lookup"><span data-stu-id="3241e-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="3241e-351">Puede ser uno de los siguientes de hello: Error, creación, en cola, Cancelar, cancelado, correcto</span><span class="sxs-lookup"><span data-stu-id="3241e-351">Can be one of hello following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="3241e-352">`feed/entry/content/properties/StatusMessage`: Mensaje de estado detallado (se aplica solo toospecific estados).</span><span class="sxs-lookup"><span data-stu-id="3241e-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="3241e-353">`feed/entry/content/properties/Progress` : progreso de la compilación (%).</span><span class="sxs-lookup"><span data-stu-id="3241e-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="3241e-354">`feed/entry/content/properties/StartTime` : hora de inicio de la compilación.</span><span class="sxs-lookup"><span data-stu-id="3241e-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="3241e-355">`feed/entry/content/properties/EndTime` : hora de finalización de la compilación.</span><span class="sxs-lookup"><span data-stu-id="3241e-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="3241e-356">`feed/entry/content/properties/ExecutionTime` : duración de la compilación.</span><span class="sxs-lookup"><span data-stu-id="3241e-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="3241e-357">`feed/entry/content/properties/ProgressStep`– Detalles acerca de la fase actual de Hola que una compilación en curso se encuentra en.</span><span class="sxs-lookup"><span data-stu-id="3241e-357">`feed/entry/content/properties/ProgressStep` – Details about hello current stage that a build in progress is in.</span></span>

<span data-ttu-id="3241e-358">Estado de compilación válido:</span><span class="sxs-lookup"><span data-stu-id="3241e-358">Valid build status:</span></span>

* <span data-ttu-id="3241e-359">Creado: se creó la entrada de solicitud de compilación.</span><span class="sxs-lookup"><span data-stu-id="3241e-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="3241e-360">En cola: la solicitud de compilación se ha desencadenado y puesto en cola.</span><span class="sxs-lookup"><span data-stu-id="3241e-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="3241e-361">Compilando: la compilación está en curso.</span><span class="sxs-lookup"><span data-stu-id="3241e-361">Building – Build is in process.</span></span>
* <span data-ttu-id="3241e-362">Success: la compilación finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="3241e-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="3241e-363">Error: la compilación finalizó con un error.</span><span class="sxs-lookup"><span data-stu-id="3241e-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="3241e-364">Cancelled: la compilación se canceló.</span><span class="sxs-lookup"><span data-stu-id="3241e-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="3241e-365">Cancelling: la compilación se está cancelando.</span><span class="sxs-lookup"><span data-stu-id="3241e-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="3241e-366">Valores válidos para el tipo de compilación:</span><span class="sxs-lookup"><span data-stu-id="3241e-366">Valid values for build type:</span></span>

* <span data-ttu-id="3241e-367">Rango: compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="3241e-367">Rank - Rank build.</span></span> <span data-ttu-id="3241e-368">(Para rango detalles de la compilación, consulte toohello documento de "Documentación de recomendación de aprendizaje de máquina API").</span><span class="sxs-lookup"><span data-stu-id="3241e-368">(For rank build details, please refer toohello "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="3241e-369">Recomendación: compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="3241e-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="3241e-370">Fbt: compilación que con frecuencia se compra junta.</span><span class="sxs-lookup"><span data-stu-id="3241e-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="3241e-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="3241e-371">OData XML</span></span>

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


### <a name="get-recommendations"></a><span data-ttu-id="3241e-372">Obtención de recomendaciones</span><span class="sxs-lookup"><span data-stu-id="3241e-372">Get recommendations</span></span>
| <span data-ttu-id="3241e-373">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="3241e-373">HTTP Method</span></span> | <span data-ttu-id="3241e-374">URI</span><span class="sxs-lookup"><span data-stu-id="3241e-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-375">GET</span><span class="sxs-lookup"><span data-stu-id="3241e-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3241e-376">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3241e-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="3241e-377">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="3241e-377">Parameter Name</span></span> | <span data-ttu-id="3241e-378">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="3241e-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-379">modelId</span><span class="sxs-lookup"><span data-stu-id="3241e-379">modelId</span></span> |<span data-ttu-id="3241e-380">Identificador único del modelo de hello (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="3241e-380">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="3241e-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="3241e-381">itemIds</span></span> |<span data-ttu-id="3241e-382">Lista separada por comas de hello elementos toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="3241e-382">Comma-separated list of hello items toorecommend for.</span></span><br><span data-ttu-id="3241e-383">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="3241e-383">Max length: 1024</span></span> |
| <span data-ttu-id="3241e-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="3241e-384">numberOfResults</span></span> |<span data-ttu-id="3241e-385">Número de resultados requeridos</span><span class="sxs-lookup"><span data-stu-id="3241e-385">Number of required results</span></span> |
| <span data-ttu-id="3241e-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="3241e-386">includeMetatadata</span></span> |<span data-ttu-id="3241e-387">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="3241e-387">Future use, always false</span></span> |
| <span data-ttu-id="3241e-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3241e-388">apiVersion</span></span> |<span data-ttu-id="3241e-389">1.0</span><span class="sxs-lookup"><span data-stu-id="3241e-389">1.0</span></span> |

<span data-ttu-id="3241e-390">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="3241e-390">**Response:**</span></span>

<span data-ttu-id="3241e-391">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3241e-391">HTTP Status code: 200</span></span>

<span data-ttu-id="3241e-392">respuesta de Hello incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="3241e-392">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="3241e-393">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3241e-393">Each entry has hello following data:</span></span>

* <span data-ttu-id="3241e-394">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="3241e-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="3241e-395">`Feed\entry\content\properties\Name`-Nombre del elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="3241e-395">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="3241e-396">`Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="3241e-396">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="3241e-397">`Feed\entry\content\properties\Reasoning`: razonamiento de la recomendación (por ejemplo, explicaciones de la recomendación).</span><span class="sxs-lookup"><span data-stu-id="3241e-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="3241e-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="3241e-398">OData XML</span></span>

<span data-ttu-id="3241e-399">respuesta de ejemplo de Hola siguiente incluye 10 elementos recomendados:</span><span class="sxs-lookup"><span data-stu-id="3241e-399">hello example response below includes 10 recommended items:</span></span>

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

### <a name="update-model"></a><span data-ttu-id="3241e-400">Actualización del modelo</span><span class="sxs-lookup"><span data-stu-id="3241e-400">Update model</span></span>
<span data-ttu-id="3241e-401">Puede actualizar la descripción del modelo de Hola u Hola Id. de compilación activa.</span><span class="sxs-lookup"><span data-stu-id="3241e-401">You can update hello model description or hello active build ID.</span></span>
<span data-ttu-id="3241e-402">*Id. de compilación activa*: cada compilación para cada modelo tiene un identificador de compilación.</span><span class="sxs-lookup"><span data-stu-id="3241e-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="3241e-403">Id. de compilación activa de Hello es primera compilación correcta Hola de cada nuevo modelo.</span><span class="sxs-lookup"><span data-stu-id="3241e-403">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="3241e-404">Una vez que tiene un identificador de compilación activa y hace que las compilaciones adicionales de Hola mismo modelo, deberá tooexplicitly establézcala como hello predeterminado Id. de compilación si desea.</span><span class="sxs-lookup"><span data-stu-id="3241e-404">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="3241e-405">Cuando utilizas recomendaciones, si no especifica el Id. de generación de Hola que desee toouse, predeterminado Hola uno se usará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3241e-405">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span>

<span data-ttu-id="3241e-406">Este mecanismo le permite - una vez que tiene un modelo de recomendación en producción - toobuild nuevos modelos y probarlas antes de promover ellos tooproduction.</span><span class="sxs-lookup"><span data-stu-id="3241e-406">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="3241e-407">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="3241e-407">HTTP Method</span></span> | <span data-ttu-id="3241e-408">URI</span><span class="sxs-lookup"><span data-stu-id="3241e-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-409">PUT</span><span class="sxs-lookup"><span data-stu-id="3241e-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3241e-410">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3241e-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3241e-411">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="3241e-411">Parameter Name</span></span> | <span data-ttu-id="3241e-412">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="3241e-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3241e-413">id</span><span class="sxs-lookup"><span data-stu-id="3241e-413">id</span></span> |<span data-ttu-id="3241e-414">Identificador único del modelo de hello (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="3241e-414">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="3241e-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3241e-415">apiVersion</span></span> |<span data-ttu-id="3241e-416">1.0</span><span class="sxs-lookup"><span data-stu-id="3241e-416">1.0</span></span> |
|  | |
| <span data-ttu-id="3241e-417">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="3241e-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="3241e-418">Tenga en cuenta que Hola XML etiquetas descripción y ActiveBuildId son opcionales.</span><span class="sxs-lookup"><span data-stu-id="3241e-418">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="3241e-419">Si no desea tooset descripción o ActiveBuildId, quite la etiqueta completa Hola.</span><span class="sxs-lookup"><span data-stu-id="3241e-419">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="3241e-420">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="3241e-420">**Response**:</span></span>

<span data-ttu-id="3241e-421">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3241e-421">HTTP Status code: 200</span></span>

<span data-ttu-id="3241e-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="3241e-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="3241e-423">Información legal</span><span class="sxs-lookup"><span data-stu-id="3241e-423">Legal</span></span>
<span data-ttu-id="3241e-424">Este documento se ofrece "tal cual".</span><span class="sxs-lookup"><span data-stu-id="3241e-424">This document is provided "as-is".</span></span> <span data-ttu-id="3241e-425">La información y las opiniones expresadas en este documento, como las direcciones URL y otras referencias a sitios web de Internet, pueden cambiar sin previo aviso.</span><span class="sxs-lookup"><span data-stu-id="3241e-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="3241e-426">Algunos ejemplos mencionados se proporcionan únicamente con fines ilustrativos y son ficticios.</span><span class="sxs-lookup"><span data-stu-id="3241e-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="3241e-427">No se pretende ninguna asociación o conexión real ni debe deducirse.</span><span class="sxs-lookup"><span data-stu-id="3241e-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="3241e-428">Este documento no proporcionan ningún derecho legal tooany la propiedad intelectual de ningún producto de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3241e-428">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="3241e-429">Puede copiar y usar este documento con fines internos y de referencia.</span><span class="sxs-lookup"><span data-stu-id="3241e-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="3241e-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3241e-430">© 2014 Microsoft.</span></span> <span data-ttu-id="3241e-431">Todos los derechos reservados.</span><span class="sxs-lookup"><span data-stu-id="3241e-431">All rights reserved.</span></span> 

