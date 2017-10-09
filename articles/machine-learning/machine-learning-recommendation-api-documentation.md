---
title: "Documentación de la API de aprendizaje recomendaciones aaaMachine | Documentos de Microsoft"
description: "Documentación de API de recomendaciones de aprendizaje de máquina de Azure para un motor de recomendaciones disponible en Microsoft Azure Marketplace de Hola."
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="2763e-103">Documentación de la API de recomendación de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="2763e-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="2763e-104">Debería empezar a usar Hola recomendaciones API cognitivos servicio en lugar de esta versión.</span><span class="sxs-lookup"><span data-stu-id="2763e-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="2763e-105">Hola recomendaciones cognitivos servicio va a sustituir este servicio y todas las características nuevas de Hola se van a desarrollar no existe.</span><span class="sxs-lookup"><span data-stu-id="2763e-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="2763e-106">Tiene nuevas funcionalidades como compatibilidad con procesamientos por lotes, un explorador de API más eficaz, una interfaz de API más limpia, una experiencia de facturación y suscripción más coherente, etc.</span><span class="sxs-lookup"><span data-stu-id="2763e-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="2763e-107">Obtenga más información sobre [migrar toohello nuevo servicio cognitivos](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="2763e-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="2763e-108">Este documento describe las API de recomendaciones de Aprendizaje automático de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2763e-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="2763e-109">1. Información general</span><span class="sxs-lookup"><span data-stu-id="2763e-109">1. General overview</span></span>
<span data-ttu-id="2763e-110">Este documento es una referencia de API.</span><span class="sxs-lookup"><span data-stu-id="2763e-110">This document is an API reference.</span></span> <span data-ttu-id="2763e-111">Debe empezar con el documento de "Azure máquina recomendación – inicio rápido de aprendizaje" Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-111">You should start with hello “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="2763e-112">Hola API de recomendaciones de aprendizaje de máquina de Azure puede dividirse en hello siguientes grupos lógicos:</span><span class="sxs-lookup"><span data-stu-id="2763e-112">hello Azure Machine Learning Recommendations API can be divided into hello following logical groups:</span></span>

* <span data-ttu-id="2763e-113"><ins>Limitaciones</ins>: Limitaciones de la API de recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="2763e-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="2763e-114"><ins>Información general</ins>: Información sobre la autenticación, el identificador URI de servicio y el control de versiones.</span><span class="sxs-lookup"><span data-stu-id="2763e-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="2763e-115"><ins>Modelo Basic</ins> -API que permiten operaciones básicas de hello toodo en modelo (por ejemplo, crear, actualizar y eliminar un modelo).</span><span class="sxs-lookup"><span data-stu-id="2763e-115"><ins>Model Basic</ins> - APIs that enable you toodo hello basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="2763e-116"><ins>Opciones avanzadas del modelo</ins> -API que permiten la información sobre los datos en el modelo de hello tooget avanzada.</span><span class="sxs-lookup"><span data-stu-id="2763e-116"><ins>Model Advanced</ins> - APIs that enable you tooget advanced data insights on hello model.</span></span>
* <span data-ttu-id="2763e-117"><ins>Modelo de reglas de negocios</ins> -API que permiten toomanage las reglas de negocios en resultados de recomendación del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-117"><ins>Model Business Rules</ins> - APIs that enable you toomanage business rules on hello model recommendation results.</span></span>
* <span data-ttu-id="2763e-118"><ins>Catálogo</ins> -API que permiten operaciones básicas de toodo en un catálogo de modelos.</span><span class="sxs-lookup"><span data-stu-id="2763e-118"><ins>Catalog</ins> - APIs that enable you toodo basic operations on a model catalog.</span></span> <span data-ttu-id="2763e-119">Un catálogo contiene información de metadatos en los elementos de Hola Hola de datos de uso.</span><span class="sxs-lookup"><span data-stu-id="2763e-119">A catalog contains metadata information on hello items of hello usage data.</span></span>
* <span data-ttu-id="2763e-120"><ins>Característica</ins> -API que permiten la visión de tooget en el elemento en el catálogo de Hola y cómo toouse este recomendaciones mejor toobuild de información.</span><span class="sxs-lookup"><span data-stu-id="2763e-120"><ins>Feature</ins> - APIs that enable tooget insights on item into hello catalog and how toouse this information toobuild better recommendations.</span></span>
* <span data-ttu-id="2763e-121"><ins>Datos de uso</ins> -API que permiten toodo operaciones básicas en los datos de uso del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-121"><ins>Usage Data</ins> - APIs that enable you toodo basic operations on hello model usage data.</span></span> <span data-ttu-id="2763e-122">Datos de uso de forma básica hello consisten de filas que incluyen pares de &#60; userId &#62; &#60; itemId &#62;.</span><span class="sxs-lookup"><span data-stu-id="2763e-122">Usage data in hello basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="2763e-123"><ins>Compilación</ins> : las API que permiten tootrigger un modelo de compilación y realizar operaciones básicas que están relacionados toothis la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-123"><ins>Build</ins> - APIs that enable you tootrigger a model build and do basic operations that are related toothis build.</span></span> <span data-ttu-id="2763e-124">Puede desencadenar una compilación de modelo una vez que tenga datos de uso valiosos.</span><span class="sxs-lookup"><span data-stu-id="2763e-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="2763e-125"><ins>Recomendación</ins> -API que permiten recomendaciones tooconsume una vez que finaliza la compilación de Hola de un modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-125"><ins>Recommendation</ins> - APIs that enable you tooconsume recommendations once hello build of a model ends.</span></span>
* <span data-ttu-id="2763e-126"><ins>Datos de usuario</ins> -API que permiten toofetch información sobre los datos de uso de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-126"><ins>User Data</ins> - APIs that enable you toofetch information on hello user usage data.</span></span>
* <span data-ttu-id="2763e-127"><ins>Las notificaciones</ins> -operaciones de tooyour API relacionadas con la API que permiten que las notificaciones de tooreceive en problemas.</span><span class="sxs-lookup"><span data-stu-id="2763e-127"><ins>Notifications</ins> - APIs that enable you tooreceive notifications on problems related tooyour API operations.</span></span> <span data-ttu-id="2763e-128">(Por ejemplo, está informando de datos de uso a través de la adquisición de datos y la mayoría de los eventos de Hola se producen errores en el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="2763e-128">(For example, you are reporting usage data via Data Acquisition and most of hello events processing are failing.</span></span> <span data-ttu-id="2763e-129">Se generará una notificación de error).</span><span class="sxs-lookup"><span data-stu-id="2763e-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="2763e-130">2. Limitaciones</span><span class="sxs-lookup"><span data-stu-id="2763e-130">2. Limitations</span></span>
* <span data-ttu-id="2763e-131">número máximo de Hola de modelos por suscripción es 10.</span><span class="sxs-lookup"><span data-stu-id="2763e-131">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="2763e-132">Hola número máximo de compilaciones por modelo es 20.</span><span class="sxs-lookup"><span data-stu-id="2763e-132">hello maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="2763e-133">número máximo de Hola de elementos que puede contener un catálogo es 100.000.</span><span class="sxs-lookup"><span data-stu-id="2763e-133">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="2763e-134">número máximo de Hola de puntos de uso que se mantienen es ~ 5 000 000.</span><span class="sxs-lookup"><span data-stu-id="2763e-134">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="2763e-135">Hola más antigua se eliminará si nuevos se cargan o se notificarán.</span><span class="sxs-lookup"><span data-stu-id="2763e-135">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="2763e-136">tamaño máximo de Hola de datos que se pueden enviar en POST (por ejemplo, importar datos del catálogo, importar datos de uso) es 200MB.</span><span class="sxs-lookup"><span data-stu-id="2763e-136">hello maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="2763e-137">número máximo de Hola de elementos que se pueden hacer al obtener recomendaciones es 150.</span><span class="sxs-lookup"><span data-stu-id="2763e-137">hello maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="2763e-138">3. API: información general</span><span class="sxs-lookup"><span data-stu-id="2763e-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="2763e-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="2763e-139">3.1.</span></span> <span data-ttu-id="2763e-140">Autenticación</span><span class="sxs-lookup"><span data-stu-id="2763e-140">Authentication</span></span>
<span data-ttu-id="2763e-141">Siga las instrucciones de Microsoft Azure Marketplace de hello relativos a la autenticación.</span><span class="sxs-lookup"><span data-stu-id="2763e-141">Please follow hello Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="2763e-142">marketplace de Hello es compatible con cualquier método de autenticación básica o OAuth de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-142">hello marketplace supports either hello Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="2763e-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-143">3.2.</span></span> <span data-ttu-id="2763e-144">URI de servicio</span><span class="sxs-lookup"><span data-stu-id="2763e-144">Service URI</span></span>
<span data-ttu-id="2763e-145">Hola URI raíz del servicio para las API de Azure Machine Learning recomendaciones hello es [aquí.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="2763e-145">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="2763e-146">URI del servicio completo Hola se expresa mediante elementos de especificación de OData de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-146">hello full service URI is expressed using elements of hello OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="2763e-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="2763e-147">3.3.</span></span> <span data-ttu-id="2763e-148">Versión de API</span><span class="sxs-lookup"><span data-stu-id="2763e-148">API version</span></span>
<span data-ttu-id="2763e-149">Al final de hello, cada llamada a la API tendrá un parámetro de consulta denominado valor apiVersion que se debe establecer too1.0.</span><span class="sxs-lookup"><span data-stu-id="2763e-149">Each API call will have, at hello end, a query parameter called apiVersion that should be set too1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="2763e-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="2763e-150">3.4.</span></span> <span data-ttu-id="2763e-151">Los Id. distinguen mayúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="2763e-151">IDs are case sensitive</span></span>
<span data-ttu-id="2763e-152">Identificadores, devueltos por cualquiera de hello API, distinguen mayúsculas de minúsculas y deben usarse como tales cuando se pasan como parámetros en llamadas posteriores a la API.</span><span class="sxs-lookup"><span data-stu-id="2763e-152">IDs, returned by any of hello APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="2763e-153">Por ejemplo, los Id. de modelo y de catálogo distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2763e-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="2763e-154">4. Calidad de recomendaciones y elementos fríos</span><span class="sxs-lookup"><span data-stu-id="2763e-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="2763e-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="2763e-155">4.1.</span></span> <span data-ttu-id="2763e-156">Calidad de recomendación</span><span class="sxs-lookup"><span data-stu-id="2763e-156">Recommendation quality</span></span>
<span data-ttu-id="2763e-157">Crear un modelo de recomendación suele ser suficiente recomendaciones de tooprovide del sistema de tooallow Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-157">Creating a recommendation model is usually enough tooallow hello system tooprovide recommendations.</span></span> <span data-ttu-id="2763e-158">No obstante, calidad de las recomendaciones varía según el uso de hello procesado y Hola cobertura del catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-158">Nevertheless, recommendation quality varies based on hello usage processed and hello coverage of hello catalog.</span></span> <span data-ttu-id="2763e-159">Por ejemplo si tiene una gran cantidad de elementos fríos (elementos sin uso significativo), sistema de hello tendrá dificultades para proporcionar una recomendación para un elemento de este tipo o utilizando un elemento de este tipo como recomendada.</span><span class="sxs-lookup"><span data-stu-id="2763e-159">For example if you have a lot of cold items (items without significant usage), hello system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="2763e-160">Problema de elemento inactivos de orden tooovercome hello, sistema de Hola permite el uso de Hola de metadatos de las recomendaciones de hello elementos tooenhance Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-160">In order tooovercome hello cold item problem, hello system allows hello use of metadata of hello items tooenhance hello recommendations.</span></span> <span data-ttu-id="2763e-161">Estos metadatos son características de tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="2763e-161">This metadata is referred tooas features.</span></span> <span data-ttu-id="2763e-162">Características típicas son el autor de un libro o el actor de una película.</span><span class="sxs-lookup"><span data-stu-id="2763e-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="2763e-163">Características son proporcionadas a través del catálogo de hello en forma de Hola de cadenas de clave/valor.</span><span class="sxs-lookup"><span data-stu-id="2763e-163">Features are provided via hello catalog in hello form of key/value strings.</span></span> <span data-ttu-id="2763e-164">Formato completo de Hola Hola del archivo de catálogo, consulte toohello [importar sección catálogo](#81-import-catalog-data).</span><span class="sxs-lookup"><span data-stu-id="2763e-164">For hello full format of hello catalog file, please refer toohello [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="2763e-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-165">4.2.</span></span> <span data-ttu-id="2763e-166">Compilación de rango</span><span class="sxs-lookup"><span data-stu-id="2763e-166">Rank build</span></span>
<span data-ttu-id="2763e-167">Características pueden mejorar el modelo de recomendación de hello, pero toodo por lo que requiere el uso de Hola de características significativos.</span><span class="sxs-lookup"><span data-stu-id="2763e-167">Features can enhance hello recommendation model, but toodo so requires hello use of meaningful features.</span></span> <span data-ttu-id="2763e-168">Con este fin se introdujo una nueva compilación, una compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="2763e-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="2763e-169">Esta compilación clasificará utilidad Hola de características.</span><span class="sxs-lookup"><span data-stu-id="2763e-169">This build will rank hello usefulness of features.</span></span> <span data-ttu-id="2763e-170">Una característica significativa es una característica con una puntuación de rango de 2 para arriba.</span><span class="sxs-lookup"><span data-stu-id="2763e-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="2763e-171">Una vez que conozca cuál de las características de hello son significativos, desencadenar una compilación de recomendación con lista de hello (o sublista) de características significativos.</span><span class="sxs-lookup"><span data-stu-id="2763e-171">After understanding which of hello features are meaningful, trigger a recommendation build with hello list (or sublist) of meaningful features.</span></span> <span data-ttu-id="2763e-172">Es posible toouse que estas características de mejora de Hola de los elementos fríos y elementos de estado.</span><span class="sxs-lookup"><span data-stu-id="2763e-172">It is possible toouse these feature for hello enhancement of both warm items and cold items.</span></span> <span data-ttu-id="2763e-173">En orden toouse para elementos semiactivos, Hola `UseFeatureInModel` se deben configurar los parámetros de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-173">In order toouse them for warm items, hello `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="2763e-174">En las características de toouse de orden para los elementos fríos, Hola `AllowColdItemPlacement` debe habilitarse el parámetro de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-174">In order toouse features for cold items, hello `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="2763e-175">Nota: No es posible tooenable `AllowColdItemPlacement` sin habilitar `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="2763e-175">Note: It is not possible tooenable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="2763e-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="2763e-176">4.3.</span></span> <span data-ttu-id="2763e-177">Razonamiento de recomendación</span><span class="sxs-lookup"><span data-stu-id="2763e-177">Recommendation reasoning</span></span>
<span data-ttu-id="2763e-178">El razonamiento de la recomendación es otro aspecto del uso de características.</span><span class="sxs-lookup"><span data-stu-id="2763e-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="2763e-179">De hecho, motor de recomendaciones de aprendizaje de máquina de Azure Hola puede utilizar la explicaciones de recomendación de características tooprovide (conocido como)</span><span class="sxs-lookup"><span data-stu-id="2763e-179">Indeed, hello Azure Machine Learning Recommendations engine can use features tooprovide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="2763e-180">Razonamiento), iniciales toomore confianza Hola recomienda elemento de consumidor de la recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-180">reasoning), leading toomore confidence in hello recommended item from hello recommendation consumer.</span></span>
<span data-ttu-id="2763e-181">tooenable razonamiento, hello `AllowFeatureCorrelation` y `ReasoningFeatureList` parámetros deben ser el programa de instalación anterior toorequesting una compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="2763e-181">tooenable reasoning, hello `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior toorequesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="2763e-182">5. Modelo básico</span><span class="sxs-lookup"><span data-stu-id="2763e-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="2763e-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="2763e-183">5.1.</span></span> <span data-ttu-id="2763e-184">Crear modelo</span><span class="sxs-lookup"><span data-stu-id="2763e-184">Create Model</span></span>
<span data-ttu-id="2763e-185">Crea una solicitud "crear modelo".</span><span class="sxs-lookup"><span data-stu-id="2763e-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="2763e-186">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-186">HTTP Method</span></span> | <span data-ttu-id="2763e-187">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-188">POST</span><span class="sxs-lookup"><span data-stu-id="2763e-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-189">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-190">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-190">Parameter Name</span></span> | <span data-ttu-id="2763e-191">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-192">modelName</span><span class="sxs-lookup"><span data-stu-id="2763e-192">modelName</span></span> |<span data-ttu-id="2763e-193">Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="2763e-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="2763e-194">Longitud máxima: 20</span><span class="sxs-lookup"><span data-stu-id="2763e-194">Max length: 20</span></span> |
| <span data-ttu-id="2763e-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-195">apiVersion</span></span> |<span data-ttu-id="2763e-196">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-196">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-197">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-197">Request Body</span></span> |<span data-ttu-id="2763e-198">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-198">NONE</span></span> |

<span data-ttu-id="2763e-199">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-199">**Response**:</span></span>

<span data-ttu-id="2763e-200">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="2763e-201">`feed/entry/content/properties/id`-Contiene el identificador del modelo Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-201">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="2763e-202">**Nota**: el Id. de modelo distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2763e-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="2763e-203">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-203">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a><span data-ttu-id="2763e-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-204">5.2.</span></span> <span data-ttu-id="2763e-205">Obtener modelo</span><span class="sxs-lookup"><span data-stu-id="2763e-205">Get Model</span></span>
<span data-ttu-id="2763e-206">Crea una solicitud "obtener modelo".</span><span class="sxs-lookup"><span data-stu-id="2763e-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="2763e-207">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-207">HTTP Method</span></span> | <span data-ttu-id="2763e-208">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-209">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="2763e-210">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-211">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-211">Parameter Name</span></span> | <span data-ttu-id="2763e-212">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-213">id</span><span class="sxs-lookup"><span data-stu-id="2763e-213">id</span></span> |<span data-ttu-id="2763e-214">Identificador único del modelo de hello (con distinción entre mayúsculas y minúsculas)</span><span class="sxs-lookup"><span data-stu-id="2763e-214">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="2763e-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-215">apiVersion</span></span> |<span data-ttu-id="2763e-216">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-216">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-217">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-217">Request Body</span></span> |<span data-ttu-id="2763e-218">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-218">NONE</span></span> |

<span data-ttu-id="2763e-219">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-219">**Response**:</span></span>

<span data-ttu-id="2763e-220">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-220">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-221">datos del modelo Hola pueden encontrarse en hello siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2763e-221">hello model data can be found under hello following elements:</span></span>

* <span data-ttu-id="2763e-222">`feed/entry/content/properties/Id`: id. único de modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="2763e-223">`feed/entry/content/properties/Name`: nombre del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="2763e-224">`feed/entry/content/properties/Date` : fecha de creación del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="2763e-225">`feed/entry/content/properties/Status` : estado del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="2763e-226">Uno de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-226">One of hello following:</span></span>
  * <span data-ttu-id="2763e-227">Created: el modelo se crea y no contiene Catálogo ni Uso.</span><span class="sxs-lookup"><span data-stu-id="2763e-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="2763e-228">ReadyForBuild: el modelo se crea y contiene Catálogo y Uso.</span><span class="sxs-lookup"><span data-stu-id="2763e-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="2763e-229">`feed/entry/content/properties/HasActiveBuild`: Indica si el modelo de Hola se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="2763e-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="2763e-230">`feed/entry/content/properties/BuildId` : id. de compilación activa del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="2763e-231">`feed/entry/content/properties/Mpr`: clasificación percentil de promedio del modelo (MPR, consulte ModelInsight para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="2763e-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="2763e-232">`feed/entry/content/properties/UserName` : nombre de usuario interno del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="2763e-233">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-233">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a><span data-ttu-id="2763e-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="2763e-234">5.3.</span></span>    <span data-ttu-id="2763e-235">Obtener todos los modelos</span><span class="sxs-lookup"><span data-stu-id="2763e-235">Get All Models</span></span>
<span data-ttu-id="2763e-236">Recupera todos los modelos del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-236">Retrieves all models of hello current user.</span></span>

| <span data-ttu-id="2763e-237">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-237">HTTP Method</span></span> | <span data-ttu-id="2763e-238">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-239">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="2763e-240">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-241">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-241">Parameter Name</span></span> | <span data-ttu-id="2763e-242">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-243">apiVersion</span></span> |<span data-ttu-id="2763e-244">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-244">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-245">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-245">Request Body</span></span> |<span data-ttu-id="2763e-246">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-246">NONE</span></span> |

<span data-ttu-id="2763e-247">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-247">**Response**:</span></span>

<span data-ttu-id="2763e-248">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="2763e-249">`feed/entry/content/properties/Id`: id. único de modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="2763e-250">`feed/entry/content/properties/Name`: nombre del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="2763e-251">`feed/entry/content/properties/Date` : fecha de creación del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="2763e-252">`feed/entry/content/properties/Status` : estado del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="2763e-253">Uno de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-253">One of hello following:</span></span>
  * <span data-ttu-id="2763e-254">Created: el modelo se crea y no contiene Catálogo ni Uso.</span><span class="sxs-lookup"><span data-stu-id="2763e-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="2763e-255">ReadyForBuild: el modelo se crea y contiene Catálogo y Uso.</span><span class="sxs-lookup"><span data-stu-id="2763e-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="2763e-256">`feed/entry/content/properties/HasActiveBuild`: Indica si el modelo de Hola se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="2763e-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="2763e-257">`feed/entry/content/properties/BuildId` : id. de compilación activa del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="2763e-258">`feed/entry/content/properties/Mpr`: MPR del modelo (consulte ModelInsight para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="2763e-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="2763e-259">`feed/entry/content/properties/UserName` : nombre de usuario interno del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="2763e-260">`feed/entry/content/properties/UsageFileNames`: lista de archivos de uso del modelo separados por coma.</span><span class="sxs-lookup"><span data-stu-id="2763e-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="2763e-261">`feed/entry/content/properties/CatalogId`: id. de catálogo del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="2763e-262">`feed/entry/content/properties/Description`: descripción del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="2763e-263">`feed/entry/content/properties/CatalogFileName` : nombre de archivo del catálogo de modelos.</span><span class="sxs-lookup"><span data-stu-id="2763e-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="2763e-264">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-264">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a><span data-ttu-id="2763e-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="2763e-265">5.4.</span></span>    <span data-ttu-id="2763e-266">Actualizar modelo</span><span class="sxs-lookup"><span data-stu-id="2763e-266">Update Model</span></span>
<span data-ttu-id="2763e-267">Puede actualizar la descripción del modelo de Hola u Hola Id. de compilación activa.</span><span class="sxs-lookup"><span data-stu-id="2763e-267">You can update hello model description or hello active build ID.</span></span><br><span data-ttu-id="2763e-268">
<ins>Id. de compilación activa</ins>: cada compilación para cada modelo tiene un identificador de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="2763e-269">Id. de compilación activa de Hello es primera compilación correcta Hola de cada nuevo modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-269">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="2763e-270">Una vez que tiene un identificador de compilación activa y hace que las compilaciones adicionales de Hola mismo modelo, deberá tooexplicitly establézcala como hello predeterminado Id. de compilación si desea.</span><span class="sxs-lookup"><span data-stu-id="2763e-270">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="2763e-271">Cuando utilizas recomendaciones, si no especifica el Id. de generación de Hola que desee toouse, predeterminado Hola uno se usará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2763e-271">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span><br>
<span data-ttu-id="2763e-272">Este mecanismo le permite - una vez que tiene un modelo de recomendación en producción - toobuild nuevos modelos y probarlas antes de promover ellos tooproduction.</span><span class="sxs-lookup"><span data-stu-id="2763e-272">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="2763e-273">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-273">HTTP Method</span></span> | <span data-ttu-id="2763e-274">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-275">PUT</span><span class="sxs-lookup"><span data-stu-id="2763e-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="2763e-276">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-277">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-277">Parameter Name</span></span> | <span data-ttu-id="2763e-278">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-279">id</span><span class="sxs-lookup"><span data-stu-id="2763e-279">id</span></span> |<span data-ttu-id="2763e-280">Identificador único del modelo de hello (con distinción entre mayúsculas y minúsculas)</span><span class="sxs-lookup"><span data-stu-id="2763e-280">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="2763e-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-281">apiVersion</span></span> |<span data-ttu-id="2763e-282">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-282">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-283">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="2763e-284">Tenga en cuenta que Hola XML etiquetas descripción y ActiveBuildId son opcionales.</span><span class="sxs-lookup"><span data-stu-id="2763e-284">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="2763e-285">Si no desea tooset descripción o ActiveBuildId, quite la etiqueta completa Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-285">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="2763e-286">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-286">**Response**:</span></span>

<span data-ttu-id="2763e-287">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="2763e-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="2763e-288">5.5.</span></span>    <span data-ttu-id="2763e-289">Eliminar modelo</span><span class="sxs-lookup"><span data-stu-id="2763e-289">Delete Model</span></span>
<span data-ttu-id="2763e-290">Elimina un modelo existente por el Id.</span><span class="sxs-lookup"><span data-stu-id="2763e-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="2763e-291">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-291">HTTP Method</span></span> | <span data-ttu-id="2763e-292">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-293">DELETE</span><span class="sxs-lookup"><span data-stu-id="2763e-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="2763e-294">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-295">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-295">Parameter Name</span></span> | <span data-ttu-id="2763e-296">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-297">id</span><span class="sxs-lookup"><span data-stu-id="2763e-297">id</span></span> |<span data-ttu-id="2763e-298">Identificador único del modelo de hello (con distinción entre mayúsculas y minúsculas)</span><span class="sxs-lookup"><span data-stu-id="2763e-298">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="2763e-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-299">apiVersion</span></span> |<span data-ttu-id="2763e-300">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-300">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-301">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-301">Request Body</span></span> |<span data-ttu-id="2763e-302">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-302">NONE</span></span> |

<span data-ttu-id="2763e-303">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-303">**Response**:</span></span>

<span data-ttu-id="2763e-304">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-304">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-305">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-305">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a><span data-ttu-id="2763e-306">6. Modelo avanzado</span><span class="sxs-lookup"><span data-stu-id="2763e-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="2763e-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="2763e-307">6.1.</span></span>    <span data-ttu-id="2763e-308">Modelo de detalles de datos</span><span class="sxs-lookup"><span data-stu-id="2763e-308">Model Data Insight</span></span>
<span data-ttu-id="2763e-309">Devuelve datos estadísticos sobre los datos de uso de Hola que este modelo se generó con.</span><span class="sxs-lookup"><span data-stu-id="2763e-309">Returns statistical data on hello usage data that this model was built with.</span></span>

<span data-ttu-id="2763e-310">Disponible solo para la compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="2763e-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="2763e-311">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-311">HTTP Method</span></span> | <span data-ttu-id="2763e-312">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-313">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="2763e-314">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-315">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-315">Parameter Name</span></span> | <span data-ttu-id="2763e-316">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-317">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-317">modelId</span></span> |<span data-ttu-id="2763e-318">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-318">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-319">apiVersion</span></span> |<span data-ttu-id="2763e-320">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-320">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-321">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-321">Request Body</span></span> |<span data-ttu-id="2763e-322">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-322">NONE</span></span> |

<span data-ttu-id="2763e-323">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-323">**Response**:</span></span>

<span data-ttu-id="2763e-324">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-324">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-325">Hola datos se devuelven como una colección de propiedades.</span><span class="sxs-lookup"><span data-stu-id="2763e-325">hello data is returned as a collection of properties.</span></span>

* <span data-ttu-id="2763e-326">`feed/entry/id/content/properties/key`-Contiene el nombre de la propiedad de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-326">`feed/entry/id/content/properties/key` - Holds hello property name.</span></span>
* <span data-ttu-id="2763e-327">`feed/entry/id/content/properties/value`-Contiene el valor de la propiedad de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-327">`feed/entry/id/content/properties/value` - Holds hello property value.</span></span>

<span data-ttu-id="2763e-328">a continuación de la tabla de Hello muestra valor Hola que representa cada clave.</span><span class="sxs-lookup"><span data-stu-id="2763e-328">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="2763e-329">Clave</span><span class="sxs-lookup"><span data-stu-id="2763e-329">Key</span></span> | <span data-ttu-id="2763e-330">Description</span><span class="sxs-lookup"><span data-stu-id="2763e-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="2763e-331">AvgItemLength</span></span> |<span data-ttu-id="2763e-332">Número promedio de usuarios distintos por elemento.</span><span class="sxs-lookup"><span data-stu-id="2763e-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="2763e-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="2763e-333">AvgUserLength</span></span> |<span data-ttu-id="2763e-334">Número promedio de usuarios distintos por usuario.</span><span class="sxs-lookup"><span data-stu-id="2763e-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="2763e-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="2763e-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="2763e-336">Número de elementos después de eliminar elementos que no se pueden modelar.</span><span class="sxs-lookup"><span data-stu-id="2763e-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="2763e-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="2763e-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="2763e-338">Número de puntos de uso después de eliminar usuarios y elementos que no se pueden modelar.</span><span class="sxs-lookup"><span data-stu-id="2763e-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="2763e-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="2763e-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="2763e-340">Número de puntos de uso después de eliminar usuarios y elementos que no se pueden modelar.</span><span class="sxs-lookup"><span data-stu-id="2763e-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="2763e-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="2763e-341">MaxItemLength</span></span> |<span data-ttu-id="2763e-342">Número de usuarios distintivos para elemento de hello más popular.</span><span class="sxs-lookup"><span data-stu-id="2763e-342">Number of distinct users for hello most popular item.</span></span> |
| <span data-ttu-id="2763e-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="2763e-343">MaxUserLength</span></span> |<span data-ttu-id="2763e-344">Número máximo de elementos distintos para un usuario.</span><span class="sxs-lookup"><span data-stu-id="2763e-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="2763e-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="2763e-345">MinItemLength</span></span> |<span data-ttu-id="2763e-346">Número máximo de usuarios distintos para un elemento.</span><span class="sxs-lookup"><span data-stu-id="2763e-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="2763e-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="2763e-347">MinUserLength</span></span> |<span data-ttu-id="2763e-348">Número mínimo de elementos distintos para un usuario.</span><span class="sxs-lookup"><span data-stu-id="2763e-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="2763e-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="2763e-349">RawNumberOfItems</span></span> |<span data-ttu-id="2763e-350">Número de elementos de archivos de uso de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-350">Number of items in hello usage files.</span></span> |
| <span data-ttu-id="2763e-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="2763e-351">RawNumberOfUsers</span></span> |<span data-ttu-id="2763e-352">Número de puntos de uso antes de cualquier eliminación.</span><span class="sxs-lookup"><span data-stu-id="2763e-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="2763e-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="2763e-353">RawNumberOfRecords</span></span> |<span data-ttu-id="2763e-354">Número de puntos de uso antes de cualquier eliminación.</span><span class="sxs-lookup"><span data-stu-id="2763e-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="2763e-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="2763e-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="2763e-356">N/D</span><span class="sxs-lookup"><span data-stu-id="2763e-356">N/A</span></span> |
| <span data-ttu-id="2763e-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="2763e-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="2763e-358">N/D</span><span class="sxs-lookup"><span data-stu-id="2763e-358">N/A</span></span> |
| <span data-ttu-id="2763e-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="2763e-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="2763e-360">N/D</span><span class="sxs-lookup"><span data-stu-id="2763e-360">N/A</span></span> |

<span data-ttu-id="2763e-361">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-361">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a><span data-ttu-id="2763e-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-362">6.2.</span></span>    <span data-ttu-id="2763e-363">Perspectiva de modelo</span><span class="sxs-lookup"><span data-stu-id="2763e-363">Model Insight</span></span>
<span data-ttu-id="2763e-364">Devuelve una visión general de modelo en la compilación active Hola o (si se proporciona) en una compilación concreta.</span><span class="sxs-lookup"><span data-stu-id="2763e-364">Returns model insight on hello active build or (if given) on a specific build.</span></span>

<span data-ttu-id="2763e-365">Disponible solo para la compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="2763e-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="2763e-366">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-366">HTTP Method</span></span> | <span data-ttu-id="2763e-367">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-368">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-368">GET</span></span> |<span data-ttu-id="2763e-369">Con identificador de compilación activa:</span><span class="sxs-lookup"><span data-stu-id="2763e-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-370">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-371">Con identificador de compilación específica:</span><span class="sxs-lookup"><span data-stu-id="2763e-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-372">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-372">Parameter Name</span></span> | <span data-ttu-id="2763e-373">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-374">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-374">modelId</span></span> |<span data-ttu-id="2763e-375">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-375">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-376">buildId</span><span class="sxs-lookup"><span data-stu-id="2763e-376">buildId</span></span> |<span data-ttu-id="2763e-377">Opcional: número que identifica una compilación correcta.</span><span class="sxs-lookup"><span data-stu-id="2763e-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="2763e-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-378">apiVersion</span></span> |<span data-ttu-id="2763e-379">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-379">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-380">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-380">Request Body</span></span> |<span data-ttu-id="2763e-381">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-381">NONE</span></span> |

<span data-ttu-id="2763e-382">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-382">**Response**:</span></span>

<span data-ttu-id="2763e-383">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-383">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-384">Hola datos se devuelven como una colección de propiedades.</span><span class="sxs-lookup"><span data-stu-id="2763e-384">hello data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="2763e-385">a continuación de la tabla de Hello muestra valor Hola que representa cada clave.</span><span class="sxs-lookup"><span data-stu-id="2763e-385">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="2763e-386">Clave</span><span class="sxs-lookup"><span data-stu-id="2763e-386">Key</span></span> | <span data-ttu-id="2763e-387">Description</span><span class="sxs-lookup"><span data-stu-id="2763e-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="2763e-388">CatalogCoverage</span></span> |<span data-ttu-id="2763e-389">¿Qué parte del catálogo de Hola puede modelarse con patrones de uso.</span><span class="sxs-lookup"><span data-stu-id="2763e-389">What part of hello catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="2763e-390">resto de Hola de elementos de hello deberá características basadas en contenido.</span><span class="sxs-lookup"><span data-stu-id="2763e-390">hello rest of hello items will need content-based features.</span></span> |
| <span data-ttu-id="2763e-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="2763e-391">Mpr</span></span> |<span data-ttu-id="2763e-392">Clasificación de percentil medio del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-392">Mean percentile ranking of hello model.</span></span> <span data-ttu-id="2763e-393">Un valor bajo es mejor.</span><span class="sxs-lookup"><span data-stu-id="2763e-393">Lower is better.</span></span> |
| <span data-ttu-id="2763e-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="2763e-394">NumberOfDimensions</span></span> |<span data-ttu-id="2763e-395">Número de dimensiones utilizado por el algoritmo de descomposición en factores de matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-395">Number of dimensions used by hello matrix factorization algorithm.</span></span> |

<span data-ttu-id="2763e-396">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-396">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a><span data-ttu-id="2763e-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="2763e-397">6.3.</span></span>    <span data-ttu-id="2763e-398">Obtener el ejemplo de modelo</span><span class="sxs-lookup"><span data-stu-id="2763e-398">Get Model Sample</span></span>
<span data-ttu-id="2763e-399">Obtiene una muestra de modelo de recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-399">Gets a sample of hello recommendation model.</span></span>

| <span data-ttu-id="2763e-400">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-400">HTTP Method</span></span> | <span data-ttu-id="2763e-401">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-402">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="2763e-403">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-404">Con identificador de compilación específica:</span><span class="sxs-lookup"><span data-stu-id="2763e-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="2763e-405">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-406">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-406">Parameter Name</span></span> | <span data-ttu-id="2763e-407">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-408">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-408">modelId</span></span> |<span data-ttu-id="2763e-409">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-409">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-410">apiVersion</span></span> |<span data-ttu-id="2763e-411">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-411">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-412">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-412">Request Body</span></span> |<span data-ttu-id="2763e-413">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-413">NONE</span></span> |

<span data-ttu-id="2763e-414">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-414">**Response**:</span></span>

<span data-ttu-id="2763e-415">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-415">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-416">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-416">OData XML</span></span>

<span data-ttu-id="2763e-417">Se devuelve una respuesta en formato de texto sin formato:</span><span class="sxs-lookup"><span data-stu-id="2763e-417">Response is returned in raw text format:</span></span>

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="2763e-418">7. Reglas de negocio de modelo</span><span class="sxs-lookup"><span data-stu-id="2763e-418">7. Model Business Rules</span></span>
<span data-ttu-id="2763e-419">Éstos son tipos de Hola de reglas admitidas:</span><span class="sxs-lookup"><span data-stu-id="2763e-419">These are hello types of rules supported:</span></span>

* <span data-ttu-id="2763e-420"><strong>Lista de bloqueadas</strong> -lista de bloqueadas permite tooprovide una lista de elementos que no desea tooreturn en los resultados de la recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-420"><strong>BlockList</strong> - BlockList enables you tooprovide a list of items that you do not want tooreturn in hello recommendation results.</span></span> 
* <span data-ttu-id="2763e-421"><strong>FeatureBlockList</strong> -lista de bloqueadas de característica permite tooblock elementos basados en valores de hello de sus características.</span><span class="sxs-lookup"><span data-stu-id="2763e-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you tooblock items based on hello values of its features.</span></span>

<span data-ttu-id="2763e-422">*No envíe más de 1000 elementos en una sola regla de lista de bloqueo. Si lo hace, es posible que se agote el tiempo de espera de la llamada. Si necesita más de 1000 elementos tooblock, puede realizar varias llamadas de lista de bloqueo.*</span><span class="sxs-lookup"><span data-stu-id="2763e-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need tooblock more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="2763e-423"><strong>Upsale</strong> -Upsale permite tooenforce elementos tooreturn en los resultados de la recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-423"><strong>Upsale</strong> - Upsale enables you tooenforce items tooreturn in hello recommendation results.</span></span>
* <span data-ttu-id="2763e-424"><strong>Lista blanca de direcciones</strong> -habilita la lista blanca se tooonly sugerir recomendaciones de una lista de elementos.</span><span class="sxs-lookup"><span data-stu-id="2763e-424"><strong>WhiteList</strong> - White List enables you tooonly suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="2763e-425"><strong>FeatureWhiteList</strong> -lista blanca de característica le permite tooonly. se recomienda elementos que tienen valores de las características específicas.</span><span class="sxs-lookup"><span data-stu-id="2763e-425"><strong>FeatureWhiteList</strong> - Feature White List enables you tooonly recommend items that have specific feature values.</span></span>
* <span data-ttu-id="2763e-426"><strong>PerSeedBlockList</strong> : por habilita la lista de bloques de inicialización tooprovide por cada elemento de una lista de elementos que no se puede devolver como resultado de la recomendación.</span><span class="sxs-lookup"><span data-stu-id="2763e-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you tooprovide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="2763e-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="2763e-427">7.1.</span></span>    <span data-ttu-id="2763e-428">Obtener reglas de modelo</span><span class="sxs-lookup"><span data-stu-id="2763e-428">Get Model Rules</span></span>
| <span data-ttu-id="2763e-429">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-429">HTTP Method</span></span> | <span data-ttu-id="2763e-430">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-431">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="2763e-432">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-433">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-433">Parameter Name</span></span> | <span data-ttu-id="2763e-434">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-435">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-435">modelId</span></span> |<span data-ttu-id="2763e-436">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-436">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-437">apiVersion</span></span> |<span data-ttu-id="2763e-438">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-438">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-439">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-439">Request Body</span></span> |<span data-ttu-id="2763e-440">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-440">NONE</span></span> |

<span data-ttu-id="2763e-441">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-441">**Response**:</span></span>

<span data-ttu-id="2763e-442">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="2763e-443">`feed/entry/content/properties/Id` : el identificador único de esta regla.</span><span class="sxs-lookup"><span data-stu-id="2763e-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="2763e-444">`feed/entry/content/properties/Type`-Tipo de regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-444">`feed/entry/content/properties/Type` - Type of hello rule.</span></span>
* <span data-ttu-id="2763e-445">`feed/entry/content/properties/Parameter` : el parámetro de regla.</span><span class="sxs-lookup"><span data-stu-id="2763e-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="2763e-446">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-446">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a><span data-ttu-id="2763e-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-447">7.2.</span></span>    <span data-ttu-id="2763e-448">Agregar regla</span><span class="sxs-lookup"><span data-stu-id="2763e-448">Add Rule</span></span>
| <span data-ttu-id="2763e-449">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-449">HTTP Method</span></span> | <span data-ttu-id="2763e-450">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-451">POST</span><span class="sxs-lookup"><span data-stu-id="2763e-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="2763e-452">ENCABEZADO</span><span class="sxs-lookup"><span data-stu-id="2763e-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="2763e-453">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-453">Parameter Name</span></span> | <span data-ttu-id="2763e-454">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-455">apiVersion</span></span> |<span data-ttu-id="2763e-456">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-456">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-457">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-457">Request Body</span></span> | |

<span data-ttu-id="2763e-458"><ins>Cada vez que proporcionar los identificadores de elementos de reglas de negocios, que seguro Hola de toouse identificador externo del elemento de hello (Hola el mismo identificador que usó en el archivo de catálogo de hello)</ins></span><span class="sxs-lookup"><span data-stu-id="2763e-458"><ins>Whenever providing Item Ids for business rules, make sure toouse hello External Id of hello item (hello same Id that you used in hello catalog file)</ins></span></span><br><span data-ttu-id="2763e-459">
<ins>tooadd una regla de lista de bloqueo:</ins></span><span class="sxs-lookup"><span data-stu-id="2763e-459">
<ins>tooadd a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="2763e-460"><ins>
<ins>una regla de FeatureBlockList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="2763e-460"><ins>
<ins>tooadd a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="2763e-461"><ins>una regla de Upsale tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="2763e-461"><ins> tooadd an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="2763e-462">
<ins>tooadd una regla de lista blanca de direcciones:</ins></span><span class="sxs-lookup"><span data-stu-id="2763e-462">
<ins>tooadd a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="2763e-463"><ins>
<ins>una regla de FeatureWhiteList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="2763e-463"><ins>
<ins>tooadd a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="2763e-464"><ins>una regla de PerSeedBlockList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="2763e-464"><ins> tooadd a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="2763e-465">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-465">**Response**:</span></span>

<span data-ttu-id="2763e-466">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-466">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-467">Hola API devuelve Hola recién creado reglas con sus detalles.</span><span class="sxs-lookup"><span data-stu-id="2763e-467">hello API returns hello newly created rule with its details.</span></span> <span data-ttu-id="2763e-468">propiedades de reglas de Hello pueden obtenerse de hello siguiendo las rutas de acceso:</span><span class="sxs-lookup"><span data-stu-id="2763e-468">hello rules property can be retrieved from hello following paths:</span></span>

* <span data-ttu-id="2763e-469">`feed/entry/content/properties/Id` : el identificador único de esta regla.</span><span class="sxs-lookup"><span data-stu-id="2763e-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="2763e-470">`feed/entry/content/properties/Type`-Tipo de regla de hello: lista de bloqueadas o Upsale.</span><span class="sxs-lookup"><span data-stu-id="2763e-470">`feed/entry/content/properties/Type` - Type of hello rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="2763e-471">`feed/entry/content/properties/Parameter` : el parámetro de regla.</span><span class="sxs-lookup"><span data-stu-id="2763e-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="2763e-472">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-472">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a><span data-ttu-id="2763e-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="2763e-473">7.3.</span></span>    <span data-ttu-id="2763e-474">Eliminar regla</span><span class="sxs-lookup"><span data-stu-id="2763e-474">Delete Rule</span></span>
| <span data-ttu-id="2763e-475">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-475">HTTP Method</span></span> | <span data-ttu-id="2763e-476">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-477">DELETE</span><span class="sxs-lookup"><span data-stu-id="2763e-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-478">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-479">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-479">Parameter Name</span></span> | <span data-ttu-id="2763e-480">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-481">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-481">modelId</span></span> |<span data-ttu-id="2763e-482">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-482">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-483">filterId</span><span class="sxs-lookup"><span data-stu-id="2763e-483">filterId</span></span> |<span data-ttu-id="2763e-484">Identificador único del filtro de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-484">Unique identifier of hello filter</span></span> |
| <span data-ttu-id="2763e-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-485">apiVersion</span></span> |<span data-ttu-id="2763e-486">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-486">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-487">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-487">Request Body</span></span> |<span data-ttu-id="2763e-488">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-488">NONE</span></span> |

<span data-ttu-id="2763e-489">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-489">**Response**:</span></span>

<span data-ttu-id="2763e-490">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="2763e-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="2763e-491">7.4.</span></span>    <span data-ttu-id="2763e-492">Eliminar todas las reglas</span><span class="sxs-lookup"><span data-stu-id="2763e-492">Delete All Rules</span></span>
| <span data-ttu-id="2763e-493">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-493">HTTP Method</span></span> | <span data-ttu-id="2763e-494">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-495">DELETE</span><span class="sxs-lookup"><span data-stu-id="2763e-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-496">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-497">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-497">Parameter Name</span></span> | <span data-ttu-id="2763e-498">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-499">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-499">modelId</span></span> |<span data-ttu-id="2763e-500">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-501">apiVersion</span></span> |<span data-ttu-id="2763e-502">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-502">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-503">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-503">Request Body</span></span> |<span data-ttu-id="2763e-504">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-504">NONE</span></span> |

<span data-ttu-id="2763e-505">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-505">**Response**:</span></span>

<span data-ttu-id="2763e-506">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="2763e-507">8. Catálogo</span><span class="sxs-lookup"><span data-stu-id="2763e-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="2763e-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="2763e-508">8.1.</span></span>    <span data-ttu-id="2763e-509">Importar datos de catálogo</span><span class="sxs-lookup"><span data-stu-id="2763e-509">Import Catalog Data</span></span>
<span data-ttu-id="2763e-510">Si va a cargar varias catálogo archivos toohello mismo modelo con varias llamadas, insertamos solo Hola nuevos elementos de catálogo.</span><span class="sxs-lookup"><span data-stu-id="2763e-510">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="2763e-511">Los elementos existentes permanecerán con valores originales de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-511">Existing items will remain with hello original values.</span></span> <span data-ttu-id="2763e-512">Los datos del catálogo no se pueden actualizar con este método.</span><span class="sxs-lookup"><span data-stu-id="2763e-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="2763e-513">datos del catálogo de Hello deben seguir Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="2763e-513">hello catalog data should follow hello following format:</span></span>

* <span data-ttu-id="2763e-514">Sin características: `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="2763e-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="2763e-515">Con características: `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="2763e-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="2763e-516">Nota: el tamaño máximo del archivo de hello es 200MB.</span><span class="sxs-lookup"><span data-stu-id="2763e-516">Note: hello maximum file size is 200MB.</span></span>

<span data-ttu-id="2763e-517">** Detalles de formato **</span><span class="sxs-lookup"><span data-stu-id="2763e-517">** Format details **</span></span>

| <span data-ttu-id="2763e-518">Nombre</span><span class="sxs-lookup"><span data-stu-id="2763e-518">Name</span></span> | <span data-ttu-id="2763e-519">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2763e-519">Mandatory</span></span> | <span data-ttu-id="2763e-520">Tipo</span><span class="sxs-lookup"><span data-stu-id="2763e-520">Type</span></span> | <span data-ttu-id="2763e-521">Description</span><span class="sxs-lookup"><span data-stu-id="2763e-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2763e-522">Id. de elemento</span><span class="sxs-lookup"><span data-stu-id="2763e-522">Item Id</span></span> |<span data-ttu-id="2763e-523">Sí</span><span class="sxs-lookup"><span data-stu-id="2763e-523">Yes</span></span> |<span data-ttu-id="2763e-524">[A-z], [a-z], [0-9], [_] &#40;Carácter de subrayado&#41;, [-] &#40;Guion&#41;</span><span class="sxs-lookup"><span data-stu-id="2763e-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="2763e-525">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="2763e-525">Max length: 50</span></span> |<span data-ttu-id="2763e-526">Identificador único de un elemento.</span><span class="sxs-lookup"><span data-stu-id="2763e-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="2763e-527">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="2763e-527">Item Name</span></span> |<span data-ttu-id="2763e-528">Sí</span><span class="sxs-lookup"><span data-stu-id="2763e-528">Yes</span></span> |<span data-ttu-id="2763e-529">Cualquier carácter alfanumérico</span><span class="sxs-lookup"><span data-stu-id="2763e-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="2763e-530">Longitud máxima: 255</span><span class="sxs-lookup"><span data-stu-id="2763e-530">Max length: 255</span></span> |<span data-ttu-id="2763e-531">Nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="2763e-531">Item name.</span></span> |
| <span data-ttu-id="2763e-532">Categoría del elemento</span><span class="sxs-lookup"><span data-stu-id="2763e-532">Item Category</span></span> |<span data-ttu-id="2763e-533">Sí</span><span class="sxs-lookup"><span data-stu-id="2763e-533">Yes</span></span> |<span data-ttu-id="2763e-534">Cualquier carácter alfanumérico</span><span class="sxs-lookup"><span data-stu-id="2763e-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="2763e-535">Longitud máxima: 255</span><span class="sxs-lookup"><span data-stu-id="2763e-535">Max length: 255</span></span> |<span data-ttu-id="2763e-536">Categoría toowhich este elemento pertenece (por ejemplo, cocina libros, series...); puede estar vacío.</span><span class="sxs-lookup"><span data-stu-id="2763e-536">Category toowhich this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="2763e-537">Descripción</span><span class="sxs-lookup"><span data-stu-id="2763e-537">Description</span></span> |<span data-ttu-id="2763e-538">No, a menos que haya características (pero puede estar vacía)</span><span class="sxs-lookup"><span data-stu-id="2763e-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="2763e-539">Cualquier carácter alfanumérico</span><span class="sxs-lookup"><span data-stu-id="2763e-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="2763e-540">Longitud máxima: 4000</span><span class="sxs-lookup"><span data-stu-id="2763e-540">Max length: 4000</span></span> |<span data-ttu-id="2763e-541">Descripción de este elemento.</span><span class="sxs-lookup"><span data-stu-id="2763e-541">Description of this item.</span></span> |
| <span data-ttu-id="2763e-542">Lista de características</span><span class="sxs-lookup"><span data-stu-id="2763e-542">Features list</span></span> |<span data-ttu-id="2763e-543">No</span><span class="sxs-lookup"><span data-stu-id="2763e-543">No</span></span> |<span data-ttu-id="2763e-544">Cualquier carácter alfanumérico</span><span class="sxs-lookup"><span data-stu-id="2763e-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="2763e-545">Longitud máxima: 4000; número máximo de características: 20</span><span class="sxs-lookup"><span data-stu-id="2763e-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="2763e-546">Lista separada por comas de nombre de la característica = valor de la característica que puede ser utilizados tooenhance recomendación del modelo; vea [temas avanzados](#2-advanced-topics) sección.</span><span class="sxs-lookup"><span data-stu-id="2763e-546">Comma-separated list of feature name=feature value that can be used tooenhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="2763e-547">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-547">HTTP Method</span></span> | <span data-ttu-id="2763e-548">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-549">POST</span><span class="sxs-lookup"><span data-stu-id="2763e-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-550">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="2763e-551">ENCABEZADO</span><span class="sxs-lookup"><span data-stu-id="2763e-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="2763e-552">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-552">Parameter Name</span></span> | <span data-ttu-id="2763e-553">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-554">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-554">modelId</span></span> |<span data-ttu-id="2763e-555">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-555">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-556">filename</span><span class="sxs-lookup"><span data-stu-id="2763e-556">filename</span></span> |<span data-ttu-id="2763e-557">Identificador textual del catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-557">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="2763e-558">Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="2763e-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="2763e-559">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="2763e-559">Max length: 50</span></span> |
| <span data-ttu-id="2763e-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-560">apiVersion</span></span> |<span data-ttu-id="2763e-561">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-561">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-562">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-562">Request Body</span></span> |<span data-ttu-id="2763e-563">Ejemplo (con características):</span><span class="sxs-lookup"><span data-stu-id="2763e-563">Example (with features):</span></span><br/><span data-ttu-id="2763e-564">2406e770-769c-4189-89de-1c9283f93a96, Clara Callan, libro, descripción del libro hello, crear = Richard Wright, publisher = Harper Flamingo Canadá, año = 2001</span><span class="sxs-lookup"><span data-stu-id="2763e-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,hello book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="2763e-565">Hola 21bf8088-b6c0-4509-870c-e1c7ac78304a, Forgetting sala: A ficción (Byzantium Book), libro, crear = Nick Bantock, publisher = Harpercollins, año = 1997</span><span class="sxs-lookup"><span data-stu-id="2763e-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="2763e-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="2763e-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="2763e-567">552a1940-21e4-4399-82bb-594b46d7ed54, retención de Animals, libro, descripción del libro hello, crear = Magnus Mills, publisher = publicación de juegos, año = 1998</span><span class="sxs-lookup"><span data-stu-id="2763e-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,hello book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="2763e-568">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-568">**Response**:</span></span>

<span data-ttu-id="2763e-569">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-569">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-570">Hola API devuelve un informe de importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-570">hello API returns a report of hello import.</span></span>

* <span data-ttu-id="2763e-571">`feed\entry\content\properties\LineCount` : número de líneas aceptadas.</span><span class="sxs-lookup"><span data-stu-id="2763e-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="2763e-572">`feed\entry\content\properties\ErrorCount`-Número de líneas que no se insertaron debido a error de tooan.</span><span class="sxs-lookup"><span data-stu-id="2763e-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="2763e-573">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-573">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a><span data-ttu-id="2763e-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-574">8.2.</span></span>    <span data-ttu-id="2763e-575">Obtener catálogo</span><span class="sxs-lookup"><span data-stu-id="2763e-575">Get Catalog</span></span>
<span data-ttu-id="2763e-576">Recupera todos los elementos del catálogo.</span><span class="sxs-lookup"><span data-stu-id="2763e-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="2763e-577">catálogo de Hello será recuperar una página a la vez.</span><span class="sxs-lookup"><span data-stu-id="2763e-577">hello catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="2763e-578">Si desea tooget elementos en un índice determinado, puede usar el parámetro de hello $skip odata.</span><span class="sxs-lookup"><span data-stu-id="2763e-578">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="2763e-579">Por ejemplo si desea que los elementos de tooget a partir de posición 100, Agregar parámetro hello $skip = 100 solicitud toohello.</span><span class="sxs-lookup"><span data-stu-id="2763e-579">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="2763e-580">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-580">HTTP Method</span></span> | <span data-ttu-id="2763e-581">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-582">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-583">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-584">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-584">Parameter Name</span></span> | <span data-ttu-id="2763e-585">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-586">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-586">modelId</span></span> |<span data-ttu-id="2763e-587">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-587">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-588">apiVersion</span></span> |<span data-ttu-id="2763e-589">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-589">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-590">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-590">Request Body</span></span> |<span data-ttu-id="2763e-591">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-591">NONE</span></span> |

<span data-ttu-id="2763e-592">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-592">**Response**:</span></span>

<span data-ttu-id="2763e-593">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-593">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-594">respuesta de Hello incluye una entrada por cada elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="2763e-594">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="2763e-595">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-595">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-596">`feed/entry/content/properties/ExternalId`-Identificador externo del elemento del catálogo, Hola uno proporcionado por el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, hello one provided by hello customer.</span></span>
* <span data-ttu-id="2763e-597">`feed/entry/content/properties/InternalId`-Catálogo Id. interno del elemento, Hola uno generadas por las recomendaciones de aprendizaje de máquina de Azure.</span><span class="sxs-lookup"><span data-stu-id="2763e-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="2763e-598">`feed/entry/content/properties/Name` : nombre de elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="2763e-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="2763e-599">`feed/entry/content/properties/Category` : categoría de elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="2763e-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="2763e-600">`feed/entry/content/properties/Description` : descripción de elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="2763e-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="2763e-601">`feed/entry/content/properties/Metadata` : metadatos de elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="2763e-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="2763e-602">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-602">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="2763e-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="2763e-603">8.3.</span></span>    <span data-ttu-id="2763e-604">Obtener elementos de catálogo por token</span><span class="sxs-lookup"><span data-stu-id="2763e-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="2763e-605">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-605">HTTP Method</span></span> | <span data-ttu-id="2763e-606">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-607">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-608">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-609">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-609">Parameter Name</span></span> | <span data-ttu-id="2763e-610">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-611">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-611">modelId</span></span> |<span data-ttu-id="2763e-612">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-612">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-613">token</span><span class="sxs-lookup"><span data-stu-id="2763e-613">token</span></span> |<span data-ttu-id="2763e-614">Símbolo (token) de nombre del elemento del catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-614">Token of hello catalog item’s name.</span></span> <span data-ttu-id="2763e-615">Debe contener al menos 3 caracteres.</span><span class="sxs-lookup"><span data-stu-id="2763e-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="2763e-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-616">apiVersion</span></span> |<span data-ttu-id="2763e-617">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-617">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-618">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-618">Request Body</span></span> |<span data-ttu-id="2763e-619">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-619">NONE</span></span> |

<span data-ttu-id="2763e-620">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-620">**Response**:</span></span>

<span data-ttu-id="2763e-621">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-621">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-622">respuesta de Hello incluye una entrada por cada elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="2763e-622">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="2763e-623">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-623">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-624">`feed/entry/content/properties/InternalId`-Catálogo Id. interno del elemento, Hola uno generadas por las recomendaciones de aprendizaje de máquina de Azure.</span><span class="sxs-lookup"><span data-stu-id="2763e-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="2763e-625">`feed/entry/content/properties/Name` : nombre de elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="2763e-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="2763e-626">`feed/entry/content/properties/Rating`: (para un uso futuro)</span><span class="sxs-lookup"><span data-stu-id="2763e-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="2763e-627">`feed/entry/content/properties/Reasoning`: (para un uso futuro)</span><span class="sxs-lookup"><span data-stu-id="2763e-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="2763e-628">`feed/entry/content/properties/Metadata`: (para un uso futuro)</span><span class="sxs-lookup"><span data-stu-id="2763e-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="2763e-629">`feed/entry/content/properties/FormattedRating` : (para un uso futuro)</span><span class="sxs-lookup"><span data-stu-id="2763e-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="2763e-630">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-630">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a><span data-ttu-id="2763e-631">9. Datos de uso</span><span class="sxs-lookup"><span data-stu-id="2763e-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="2763e-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="2763e-632">9.1.</span></span>    <span data-ttu-id="2763e-633">Importar datos de uso</span><span class="sxs-lookup"><span data-stu-id="2763e-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="2763e-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="2763e-634">9.1.1.</span></span> <span data-ttu-id="2763e-635">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="2763e-635">Uploading File</span></span>
<span data-ttu-id="2763e-636">Esta sección se muestra cómo los datos de uso de tooupload mediante un archivo.</span><span class="sxs-lookup"><span data-stu-id="2763e-636">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="2763e-637">Puede llamar a esta API varias veces con datos de uso.</span><span class="sxs-lookup"><span data-stu-id="2763e-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="2763e-638">Todos los datos de uso se guardarán para todas las llamadas.</span><span class="sxs-lookup"><span data-stu-id="2763e-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="2763e-639">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-639">HTTP Method</span></span> | <span data-ttu-id="2763e-640">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-641">POST</span><span class="sxs-lookup"><span data-stu-id="2763e-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-642">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-643">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-643">Parameter Name</span></span> | <span data-ttu-id="2763e-644">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-645">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-645">modelId</span></span> |<span data-ttu-id="2763e-646">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-646">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-647">filename</span><span class="sxs-lookup"><span data-stu-id="2763e-647">filename</span></span> |<span data-ttu-id="2763e-648">Identificador textual del catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-648">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="2763e-649">Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="2763e-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="2763e-650">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="2763e-650">Max length: 50</span></span> |
| <span data-ttu-id="2763e-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-651">apiVersion</span></span> |<span data-ttu-id="2763e-652">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-652">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-653">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-653">Request Body</span></span> |<span data-ttu-id="2763e-654">Datos de uso.</span><span class="sxs-lookup"><span data-stu-id="2763e-654">Usage data.</span></span> <span data-ttu-id="2763e-655">Formato:</span><span class="sxs-lookup"><span data-stu-id="2763e-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="2763e-656">Nombre</span><span class="sxs-lookup"><span data-stu-id="2763e-656">Name</span></span></th><th><span data-ttu-id="2763e-657">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2763e-657">Mandatory</span></span></th><th><span data-ttu-id="2763e-658">Tipo</span><span class="sxs-lookup"><span data-stu-id="2763e-658">Type</span></span></th><th><span data-ttu-id="2763e-659">Description</span><span class="sxs-lookup"><span data-stu-id="2763e-659">Description</span></span></th></tr><tr><td><span data-ttu-id="2763e-660">Id. de usuario</span><span class="sxs-lookup"><span data-stu-id="2763e-660">User Id</span></span></td><td><span data-ttu-id="2763e-661">Sí</span><span class="sxs-lookup"><span data-stu-id="2763e-661">Yes</span></span></td><td><span data-ttu-id="2763e-662">[A-z], [a-z], [0-9], [_] &#40;Carácter de subrayado&#41;, [-] &#40;Guion&#41;</span><span class="sxs-lookup"><span data-stu-id="2763e-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="2763e-663">Longitud máxima: 255</span><span class="sxs-lookup"><span data-stu-id="2763e-663">Max length: 255</span></span> </td><td><span data-ttu-id="2763e-664">Identificador único de un usuario.</span><span class="sxs-lookup"><span data-stu-id="2763e-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="2763e-665">Id. de elemento</span><span class="sxs-lookup"><span data-stu-id="2763e-665">Item Id</span></span></td><td><span data-ttu-id="2763e-666">Sí</span><span class="sxs-lookup"><span data-stu-id="2763e-666">Yes</span></span></td><td><span data-ttu-id="2763e-667">[A-z], [a-z], [0-9], [&#95;] &#40;Carácter de subrayado&#41;, [-] &#40;Guion&#41;</span><span class="sxs-lookup"><span data-stu-id="2763e-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="2763e-668">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="2763e-668">Max length: 50</span></span></td><td><span data-ttu-id="2763e-669">Identificador único de un elemento.</span><span class="sxs-lookup"><span data-stu-id="2763e-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="2763e-670">Hora</span><span class="sxs-lookup"><span data-stu-id="2763e-670">Time</span></span></td><td><span data-ttu-id="2763e-671">No</span><span class="sxs-lookup"><span data-stu-id="2763e-671">No</span></span></td><td><span data-ttu-id="2763e-672">La fecha en este formato: AAAA/MM/DDTHH:MM:SS (por ejemplo, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="2763e-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="2763e-673">Hora de los datos.</span><span class="sxs-lookup"><span data-stu-id="2763e-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="2763e-674">Evento</span><span class="sxs-lookup"><span data-stu-id="2763e-674">Event</span></span></td><td><span data-ttu-id="2763e-675">No, si se suministra también se debe colocar la fecha</span><span class="sxs-lookup"><span data-stu-id="2763e-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="2763e-676">Uno de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-676">One of hello following:</span></span><br><span data-ttu-id="2763e-677">• Click</span><span class="sxs-lookup"><span data-stu-id="2763e-677">• Click</span></span><br><span data-ttu-id="2763e-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="2763e-678">• RecommendationClick</span></span><br><span data-ttu-id="2763e-679">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="2763e-679">•    AddShopCart</span></span><br><span data-ttu-id="2763e-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="2763e-680">• RemoveShopCart</span></span><br><span data-ttu-id="2763e-681">• compra</span><span class="sxs-lookup"><span data-stu-id="2763e-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="2763e-682">Tamaño de archivo máximo: 200 MB</span><span class="sxs-lookup"><span data-stu-id="2763e-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="2763e-683">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="2763e-684">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-684">**Response**:</span></span>

<span data-ttu-id="2763e-685">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="2763e-686">`Feed\entry\content\properties\LineCount` : número de líneas aceptadas.</span><span class="sxs-lookup"><span data-stu-id="2763e-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="2763e-687">`Feed\entry\content\properties\ErrorCount`-Número de líneas que no se insertaron debido a error de tooan.</span><span class="sxs-lookup"><span data-stu-id="2763e-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="2763e-688">`Feed\entry\content\properties\FileId` : identificador de archivo.</span><span class="sxs-lookup"><span data-stu-id="2763e-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="2763e-689">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-689">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="2763e-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-690">9.1.2.</span></span> <span data-ttu-id="2763e-691">Uso de la adquisición de datos</span><span class="sxs-lookup"><span data-stu-id="2763e-691">Using Data Acquisition</span></span>
<span data-ttu-id="2763e-692">Esta sección muestra cómo toosend eventos real hora de recomendaciones de aprendizaje de máquina tooAzure, normalmente desde su sitio Web.</span><span class="sxs-lookup"><span data-stu-id="2763e-692">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="2763e-693">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-693">HTTP Method</span></span> | <span data-ttu-id="2763e-694">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-695">POST</span><span class="sxs-lookup"><span data-stu-id="2763e-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="2763e-696">ENCABEZADO</span><span class="sxs-lookup"><span data-stu-id="2763e-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="2763e-697">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-697">Parameter Name</span></span> | <span data-ttu-id="2763e-698">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-699">apiVersion</span></span> |<span data-ttu-id="2763e-700">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-700">1.0</span></span> |
| <span data-ttu-id="2763e-701">Request body</span><span class="sxs-lookup"><span data-stu-id="2763e-701">Request body</span></span> |<span data-ttu-id="2763e-702">Entrada de datos de evento para cada evento que desee toosend.</span><span class="sxs-lookup"><span data-stu-id="2763e-702">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="2763e-703">Debe enviar para la misma sesión de usuario o el Examinador de Hola Hola mismo identificador en el campo de SessionId Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-703">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="2763e-704">(Vea el ejemplo del cuerpo de evento aparece a continuación).</span><span class="sxs-lookup"><span data-stu-id="2763e-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="2763e-705">Ejemplo para evento 'Click':</span><span class="sxs-lookup"><span data-stu-id="2763e-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="2763e-706">Ejemplo para evento 'RecommendationClick':</span><span class="sxs-lookup"><span data-stu-id="2763e-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="2763e-707">Ejemplo para evento 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="2763e-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="2763e-708">Ejemplo para evento 'RemoveShopCart':</span><span class="sxs-lookup"><span data-stu-id="2763e-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="2763e-709">Ejemplo para el evento “Purchase”:</span><span class="sxs-lookup"><span data-stu-id="2763e-709">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="2763e-710">Ejemplo con envío de 2 eventos, 'Click' y 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="2763e-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="2763e-711">**Respuesta**: código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="2763e-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-712">9.2.</span></span>    <span data-ttu-id="2763e-713">Mostrar archivos de uso de modelo</span><span class="sxs-lookup"><span data-stu-id="2763e-713">List Model Usage Files</span></span>
<span data-ttu-id="2763e-714">Recupera los metadatos de todos los archivos de uso de modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="2763e-715">Hello uso de archivos que recupera una página a la vez.</span><span class="sxs-lookup"><span data-stu-id="2763e-715">hello usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="2763e-716">Cada página contiene 100 elementos.</span><span class="sxs-lookup"><span data-stu-id="2763e-716">Each page containes 100 items.</span></span> <span data-ttu-id="2763e-717">Si desea tooget elementos en un índice determinado, puede usar el parámetro de hello $skip odata.</span><span class="sxs-lookup"><span data-stu-id="2763e-717">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="2763e-718">Por ejemplo si desea que los elementos de tooget a partir de posición 100, Agregar parámetro hello $skip = 100 solicitud toohello.</span><span class="sxs-lookup"><span data-stu-id="2763e-718">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="2763e-719">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-719">HTTP Method</span></span> | <span data-ttu-id="2763e-720">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-721">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-722">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-723">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-723">Parameter Name</span></span> | <span data-ttu-id="2763e-724">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="2763e-725">forModelId</span></span> |<span data-ttu-id="2763e-726">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-726">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-727">apiVersion</span></span> |<span data-ttu-id="2763e-728">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-728">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-729">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-729">Request Body</span></span> |<span data-ttu-id="2763e-730">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-730">NONE</span></span> |

<span data-ttu-id="2763e-731">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-731">**Response**:</span></span>

<span data-ttu-id="2763e-732">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-732">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-733">respuesta de Hello incluye una entrada por cada archivo de uso.</span><span class="sxs-lookup"><span data-stu-id="2763e-733">hello response includes one entry per usage file.</span></span> <span data-ttu-id="2763e-734">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-734">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-735">`feed\entry\content\properties\Id`: id. de archivo de uso.</span><span class="sxs-lookup"><span data-stu-id="2763e-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="2763e-736">`feed\entry\content\properties\Length` : longitud del archivo uso en MB.</span><span class="sxs-lookup"><span data-stu-id="2763e-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="2763e-737">`feed\entry\content\properties\DateModified`-Fecha cuando se creó el archivo de uso de hello.</span><span class="sxs-lookup"><span data-stu-id="2763e-737">`feed\entry\content\properties\DateModified` - Date when hello usage file was created.</span></span>
* <span data-ttu-id="2763e-738">`feed\entry\content\properties\UseInModel`-Si se usan archivos de uso de hello en el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-738">`feed\entry\content\properties\UseInModel` - Whether hello usage file is used in hello model.</span></span>

<span data-ttu-id="2763e-739">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-739">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a><span data-ttu-id="2763e-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="2763e-740">9.3.</span></span>    <span data-ttu-id="2763e-741">Obtener estadísticas de uso</span><span class="sxs-lookup"><span data-stu-id="2763e-741">Get Usage Statistics</span></span>
<span data-ttu-id="2763e-742">Obtiene estadísticas de uso.</span><span class="sxs-lookup"><span data-stu-id="2763e-742">Gets usage statistics.</span></span>

| <span data-ttu-id="2763e-743">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-743">HTTP Method</span></span> | <span data-ttu-id="2763e-744">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-745">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-746">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-747">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-747">Parameter Name</span></span> | <span data-ttu-id="2763e-748">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-749">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-749">modelId</span></span> |<span data-ttu-id="2763e-750">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-750">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-751">startDate</span><span class="sxs-lookup"><span data-stu-id="2763e-751">startDate</span></span> |<span data-ttu-id="2763e-752">Fecha de inicio.</span><span class="sxs-lookup"><span data-stu-id="2763e-752">Start date.</span></span> <span data-ttu-id="2763e-753">Formato: aaaa/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="2763e-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="2763e-754">endDate</span><span class="sxs-lookup"><span data-stu-id="2763e-754">endDate</span></span> |<span data-ttu-id="2763e-755">Fecha de fin.</span><span class="sxs-lookup"><span data-stu-id="2763e-755">End date.</span></span> <span data-ttu-id="2763e-756">Formato: aaaa/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="2763e-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="2763e-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="2763e-757">eventTypes</span></span> |<span data-ttu-id="2763e-758">Cadena separada por comas de evento tipos o null tooget todos los eventos</span><span class="sxs-lookup"><span data-stu-id="2763e-758">Comma-separated string of event types or null tooget all events</span></span> |
| <span data-ttu-id="2763e-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-759">apiVersion</span></span> |<span data-ttu-id="2763e-760">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-760">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-761">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-761">Request Body</span></span> |<span data-ttu-id="2763e-762">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-762">NONE</span></span> |

<span data-ttu-id="2763e-763">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-763">**Response**:</span></span>

<span data-ttu-id="2763e-764">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-764">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-765">Una colección de elementos de clave y valor.</span><span class="sxs-lookup"><span data-stu-id="2763e-765">A collection of key/value elements.</span></span> <span data-ttu-id="2763e-766">Cada uno de ellos contiene la suma de Hola de eventos para un tipo de evento concreto agrupadas por hora.</span><span class="sxs-lookup"><span data-stu-id="2763e-766">Each one contains hello sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="2763e-767">`feed\entry[i]\content\properties\Key`-Contiene la hora de hello (agrupado por hora) y el tipo de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-767">`feed\entry[i]\content\properties\Key` - Contains hello time (grouped by hour) and hello event type.</span></span>
* <span data-ttu-id="2763e-768">`feed\entry[i]\content\properties\Value` : recuento total de eventos.</span><span class="sxs-lookup"><span data-stu-id="2763e-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="2763e-769">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-769">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="2763e-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="2763e-770">9.4.</span></span>    <span data-ttu-id="2763e-771">Obtener ejemplo de archivo de uso</span><span class="sxs-lookup"><span data-stu-id="2763e-771">Get Usage File Sample</span></span>
<span data-ttu-id="2763e-772">Recupera Hola 2KB primer uso de contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="2763e-772">Retrieves hello first 2KB of usage file content.</span></span>

| <span data-ttu-id="2763e-773">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-773">HTTP Method</span></span> | <span data-ttu-id="2763e-774">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-775">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-776">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-777">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-777">Parameter Name</span></span> | <span data-ttu-id="2763e-778">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-779">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-779">modelId</span></span> |<span data-ttu-id="2763e-780">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-780">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-781">fileId</span><span class="sxs-lookup"><span data-stu-id="2763e-781">fileId</span></span> |<span data-ttu-id="2763e-782">Identificador único del archivo de uso del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-782">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="2763e-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-783">apiVersion</span></span> |<span data-ttu-id="2763e-784">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-784">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-785">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-785">Request Body</span></span> |<span data-ttu-id="2763e-786">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-786">NONE</span></span> |

<span data-ttu-id="2763e-787">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-787">**Response**:</span></span>

<span data-ttu-id="2763e-788">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-788">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-789">Se devuelve una respuesta en formato de texto sin formato:</span><span class="sxs-lookup"><span data-stu-id="2763e-789">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a><span data-ttu-id="2763e-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="2763e-790">9.5.</span></span>    <span data-ttu-id="2763e-791">Obtener el archivo de uso de modelo</span><span class="sxs-lookup"><span data-stu-id="2763e-791">Get Model Usage File</span></span>
<span data-ttu-id="2763e-792">Recupera todo el contenido del archivo de uso de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-792">Retrieves hello full content of hello usage file.</span></span>

| <span data-ttu-id="2763e-793">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-793">HTTP Method</span></span> | <span data-ttu-id="2763e-794">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-795">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-796">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-797">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-797">Parameter Name</span></span> | <span data-ttu-id="2763e-798">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-799">mId</span><span class="sxs-lookup"><span data-stu-id="2763e-799">mid</span></span> |<span data-ttu-id="2763e-800">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-800">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-801">fid</span><span class="sxs-lookup"><span data-stu-id="2763e-801">fid</span></span> |<span data-ttu-id="2763e-802">Identificador único del archivo de uso del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-802">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="2763e-803">descargar</span><span class="sxs-lookup"><span data-stu-id="2763e-803">download</span></span> |<span data-ttu-id="2763e-804">1</span><span class="sxs-lookup"><span data-stu-id="2763e-804">1</span></span> |
| <span data-ttu-id="2763e-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-805">apiVersion</span></span> |<span data-ttu-id="2763e-806">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-806">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-807">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-807">Request Body</span></span> |<span data-ttu-id="2763e-808">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-808">NONE</span></span> |

<span data-ttu-id="2763e-809">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-809">**Response**:</span></span>

<span data-ttu-id="2763e-810">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-810">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-811">Se devuelve una respuesta en formato de texto sin formato:</span><span class="sxs-lookup"><span data-stu-id="2763e-811">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a><span data-ttu-id="2763e-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="2763e-812">9.6.</span></span>    <span data-ttu-id="2763e-813">Eliminar archivo de uso</span><span class="sxs-lookup"><span data-stu-id="2763e-813">Delete Usage File</span></span>
<span data-ttu-id="2763e-814">Elimina el archivo de uso de hello modelo especificado.</span><span class="sxs-lookup"><span data-stu-id="2763e-814">Deletes hello specified model usage file.</span></span>

| <span data-ttu-id="2763e-815">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-815">HTTP Method</span></span> | <span data-ttu-id="2763e-816">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-817">DELETE</span><span class="sxs-lookup"><span data-stu-id="2763e-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-818">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-819">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-819">Parameter Name</span></span> | <span data-ttu-id="2763e-820">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-821">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-821">modelId</span></span> |<span data-ttu-id="2763e-822">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-822">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-823">fileId</span><span class="sxs-lookup"><span data-stu-id="2763e-823">fileId</span></span> |<span data-ttu-id="2763e-824">Identificador único de hello archivo toobe eliminado</span><span class="sxs-lookup"><span data-stu-id="2763e-824">Unique identifier of hello file toobe deleted</span></span> |
| <span data-ttu-id="2763e-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-825">apiVersion</span></span> |<span data-ttu-id="2763e-826">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-826">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-827">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-827">Request Body</span></span> |<span data-ttu-id="2763e-828">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-828">NONE</span></span> |

<span data-ttu-id="2763e-829">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-829">**Response**:</span></span>

<span data-ttu-id="2763e-830">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="2763e-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="2763e-831">9.7.</span></span>    <span data-ttu-id="2763e-832">Eliminar todos los archivos de uso</span><span class="sxs-lookup"><span data-stu-id="2763e-832">Delete All Usage Files</span></span>
<span data-ttu-id="2763e-833">Elimina todos los archivos de uso del modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="2763e-834">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-834">HTTP Method</span></span> | <span data-ttu-id="2763e-835">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-836">DELETE</span><span class="sxs-lookup"><span data-stu-id="2763e-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-837">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-838">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-838">Parameter Name</span></span> | <span data-ttu-id="2763e-839">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-840">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-840">modelId</span></span> |<span data-ttu-id="2763e-841">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-841">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-842">apiVersion</span></span> |<span data-ttu-id="2763e-843">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-843">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-844">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-844">Request Body</span></span> |<span data-ttu-id="2763e-845">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-845">NONE</span></span> |

<span data-ttu-id="2763e-846">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-846">**Response**:</span></span>

<span data-ttu-id="2763e-847">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="2763e-848">10. Características</span><span class="sxs-lookup"><span data-stu-id="2763e-848">10. Features</span></span>
<span data-ttu-id="2763e-849">Esta sección muestra cómo tooretrieve característica información, como características de hello importado y sus valores, su clasificación, y cuando se ha asignado este rango.</span><span class="sxs-lookup"><span data-stu-id="2763e-849">This section shows how tooretrieve feature information, such as hello imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="2763e-850">Características se importan como parte de datos del catálogo de hello y, a continuación, su rango está asociado cuando se realiza una compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="2763e-850">Features are imported as part of hello catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="2763e-851">Rango en la característica puede cambiar correspondiente patrón toohello de datos de uso y el tipo de elementos.</span><span class="sxs-lookup"><span data-stu-id="2763e-851">Feature rank can change according toohello pattern of usage data and type of items.</span></span> <span data-ttu-id="2763e-852">Pero para los elementos/uso coherente, rango de Hola que debería tener sólo pequeñas fluctuaciones.</span><span class="sxs-lookup"><span data-stu-id="2763e-852">But for consistent usage/items, hello rank should have only small fluctuations.</span></span>
<span data-ttu-id="2763e-853">rango de Hola de características es un número no negativo.</span><span class="sxs-lookup"><span data-stu-id="2763e-853">hello rank of features is a non-negative number.</span></span> <span data-ttu-id="2763e-854">Hello número 0 significa que no se clasifican esa característica hello (ocurre si se invoca esta finalización toohello anteriores de API de la primera compilación rank de hello).</span><span class="sxs-lookup"><span data-stu-id="2763e-854">hello  number 0 means that hello feature was not ranked (happens if you invoke this API prior toohello completion of hello first rank build).</span></span> <span data-ttu-id="2763e-855">fecha de Hello en el que se atribuye rango Hola se denomina actualización de puntuación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-855">hello date at which hello rank was attributed is called hello score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="2763e-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="2763e-856">10.1.</span></span> <span data-ttu-id="2763e-857">Obtener información de características (para la última compilación de rango)</span><span class="sxs-lookup"><span data-stu-id="2763e-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="2763e-858">Recupera información de la función hello, incluida la clasificación de hello última rank compilación correcta.</span><span class="sxs-lookup"><span data-stu-id="2763e-858">Retrieves hello feature information, including ranking, for hello last successful rank build.</span></span>

| <span data-ttu-id="2763e-859">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-859">HTTP Method</span></span> | <span data-ttu-id="2763e-860">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-861">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-862">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-863">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-863">Parameter Name</span></span> | <span data-ttu-id="2763e-864">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-865">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-865">modelId</span></span> |<span data-ttu-id="2763e-866">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-866">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="2763e-867">samplingSize</span></span> |<span data-ttu-id="2763e-868">Número de valores tooinclude para cada característica según toohello datos presentes en el catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-868">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span> <br/><span data-ttu-id="2763e-869">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="2763e-869">Possible values are:</span></span><br> <span data-ttu-id="2763e-870">-1 - Todas las muestras.</span><span class="sxs-lookup"><span data-stu-id="2763e-870">-1 - All samples.</span></span> <br><span data-ttu-id="2763e-871">0: sin muestreo.</span><span class="sxs-lookup"><span data-stu-id="2763e-871">0 - No sampling.</span></span> <br><span data-ttu-id="2763e-872">N: se devuelven N muestras para cada nombre de característica.</span><span class="sxs-lookup"><span data-stu-id="2763e-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="2763e-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-873">apiVersion</span></span> |<span data-ttu-id="2763e-874">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-874">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-875">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-875">Request Body</span></span> |<span data-ttu-id="2763e-876">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-876">NONE</span></span> |

<span data-ttu-id="2763e-877">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-877">**Response**:</span></span>

<span data-ttu-id="2763e-878">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-878">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-879">respuesta de Hello contiene una lista de entradas de información de característica.</span><span class="sxs-lookup"><span data-stu-id="2763e-879">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="2763e-880">Cada entrada contiene:</span><span class="sxs-lookup"><span data-stu-id="2763e-880">Each entry contains:</span></span>

* <span data-ttu-id="2763e-881">`feed/entry/content/m:properties/d:Name` : nombre de la característica.</span><span class="sxs-lookup"><span data-stu-id="2763e-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="2763e-882">`feed/entry/content/m:properties/d:RankUpdateDate`-Fecha de en qué Hola rango en la característica de toothis asignado, conocido como</span><span class="sxs-lookup"><span data-stu-id="2763e-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="2763e-883">característica de actualización de puntuación.</span><span class="sxs-lookup"><span data-stu-id="2763e-883">score freshness feature.</span></span> <span data-ttu-id="2763e-884">Una fecha histórica ('0001-01-01T00:00:00') significa que no se ha realizado ninguna compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="2763e-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="2763e-885">`feed/entry/content/m:properties/d:Rank`: rango de característica (flotante).</span><span class="sxs-lookup"><span data-stu-id="2763e-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="2763e-886">Un rango de 2.0 para arriba se considera una buena característica.</span><span class="sxs-lookup"><span data-stu-id="2763e-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="2763e-887">`feed/entry/content/m:properties/d:SampleValues`-Lista separados por comas de valores de tamaño de muestreo toohello solicitado.</span><span class="sxs-lookup"><span data-stu-id="2763e-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="2763e-888">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="2763e-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-889">10.2.</span></span> <span data-ttu-id="2763e-890">Obtener información de características (para una compilación de rango específica)</span><span class="sxs-lookup"><span data-stu-id="2763e-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="2763e-891">Recupera información de característica de hello, incluidos Hola de categoría para una compilación de rango específica.</span><span class="sxs-lookup"><span data-stu-id="2763e-891">Retrieves hello feature information, including hello ranking for a specific rank build.</span></span>

| <span data-ttu-id="2763e-892">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-892">HTTP Method</span></span> | <span data-ttu-id="2763e-893">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-894">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-895">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-896">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-896">Parameter Name</span></span> | <span data-ttu-id="2763e-897">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-898">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-898">modelId</span></span> |<span data-ttu-id="2763e-899">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-899">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="2763e-900">samplingSize</span></span> |<span data-ttu-id="2763e-901">Número de valores tooinclude para cada característica según toohello datos presentes en el catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-901">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span><br/> <span data-ttu-id="2763e-902">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="2763e-902">Possible values are:</span></span><br> <span data-ttu-id="2763e-903">-1 - Todas las muestras.</span><span class="sxs-lookup"><span data-stu-id="2763e-903">-1 - All samples.</span></span> <br><span data-ttu-id="2763e-904">0: sin muestreo.</span><span class="sxs-lookup"><span data-stu-id="2763e-904">0 - No sampling.</span></span> <br><span data-ttu-id="2763e-905">N: se devuelven N muestras para cada nombre de característica.</span><span class="sxs-lookup"><span data-stu-id="2763e-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="2763e-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="2763e-906">rankBuildId</span></span> |<span data-ttu-id="2763e-907">Identificador único de compilación de rango de Hola o -1 para la última compilación de rango Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-907">Unique identifier of hello rank build or -1 for hello last rank build</span></span> |
| <span data-ttu-id="2763e-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-908">apiVersion</span></span> |<span data-ttu-id="2763e-909">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-909">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-910">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-910">Request Body</span></span> |<span data-ttu-id="2763e-911">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-911">NONE</span></span> |

<span data-ttu-id="2763e-912">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-912">**Response**:</span></span>

<span data-ttu-id="2763e-913">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-913">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-914">respuesta de Hello contiene una lista de entradas de información de característica.</span><span class="sxs-lookup"><span data-stu-id="2763e-914">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="2763e-915">Cada entrada contiene:</span><span class="sxs-lookup"><span data-stu-id="2763e-915">Each entry contains:</span></span>

* <span data-ttu-id="2763e-916">`feed/entry/content/m:properties/d:Name` : nombre de la característica.</span><span class="sxs-lookup"><span data-stu-id="2763e-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="2763e-917">`feed/entry/content/m:properties/d:RankUpdateDate`-Fecha de en qué Hola rango en la característica de toothis asignado, conocido como</span><span class="sxs-lookup"><span data-stu-id="2763e-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="2763e-918">característica de actualización de puntuación.</span><span class="sxs-lookup"><span data-stu-id="2763e-918">score freshness feature.</span></span> <span data-ttu-id="2763e-919">Una fecha histórica ('0001-01-01T00:00:00') significa que no se ha realizado ninguna compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="2763e-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="2763e-920">`feed/entry/content/m:properties/d:Rank`: rango de característica (flotante).</span><span class="sxs-lookup"><span data-stu-id="2763e-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="2763e-921">Un rango de 2.0 para arriba se considera una buena característica.</span><span class="sxs-lookup"><span data-stu-id="2763e-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="2763e-922">`feed/entry/content/m:properties/d:SampleValues`-Lista separados por comas de valores de tamaño de muestreo toohello solicitado.</span><span class="sxs-lookup"><span data-stu-id="2763e-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="2763e-923">OData</span><span class="sxs-lookup"><span data-stu-id="2763e-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a><span data-ttu-id="2763e-924">11. Compilación</span><span class="sxs-lookup"><span data-stu-id="2763e-924">11. Build</span></span>
  <span data-ttu-id="2763e-925">Esta sección explica Hola distintas API relacionadas con toobuilds.</span><span class="sxs-lookup"><span data-stu-id="2763e-925">This section explains hello different APIs related toobuilds.</span></span> <span data-ttu-id="2763e-926">Hay tres tipos de compilación: una compilación de recomendación, una compilación de rango y una compilación FBT (artículos que con frecuencia se compran juntos).</span><span class="sxs-lookup"><span data-stu-id="2763e-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="2763e-927">propósito de la compilación de Hello recomendación es toogenerate usa un modelo de recomendación para realizar predicciones.</span><span class="sxs-lookup"><span data-stu-id="2763e-927">hello recommendation build's purpose is toogenerate a recommendation model used for predictions.</span></span> <span data-ttu-id="2763e-928">Las predicciones (para este tipo de compilación) se presentan en dos modos:</span><span class="sxs-lookup"><span data-stu-id="2763e-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="2763e-929">I2I - también conocida como</span><span class="sxs-lookup"><span data-stu-id="2763e-929">I2I - a.k.a.</span></span> <span data-ttu-id="2763e-930">Elemento recomendaciones tooItem: un elemento o una lista de elementos de esta opción predecirá una lista de elementos que son probable toobe de gran interés.</span><span class="sxs-lookup"><span data-stu-id="2763e-930">Item tooItem recommendations - given an item or a list of items this option will predict a list of items that are likely toobe of high interest.</span></span>
* <span data-ttu-id="2763e-931">U2I - también conocida como</span><span class="sxs-lookup"><span data-stu-id="2763e-931">U2I - a.k.a.</span></span> <span data-ttu-id="2763e-932">Recomendaciones de usuario tooItem - dadas un identificador de usuario (y, opcionalmente, una lista de elementos) esta opción predecirá una lista de elementos que son probable toobe interesa hello tiene el usuario (y sus opciones adicionales de elementos).</span><span class="sxs-lookup"><span data-stu-id="2763e-932">User tooItem recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely toobe of high interest for hello given user (and its additional choice of items).</span></span> <span data-ttu-id="2763e-933">recomendaciones de Hello U2I se basan en el historial de Hola de elementos que eran de interés para el usuario de hello tiempo toohello Hola modelo se generó.</span><span class="sxs-lookup"><span data-stu-id="2763e-933">hello U2I recommendations are based on hello history of items that were of interest for hello user up toohello time hello model was built.</span></span>

<span data-ttu-id="2763e-934">Un rango es una técnica generación que le permite toolearn acerca de la utilidad de Hola de sus características.</span><span class="sxs-lookup"><span data-stu-id="2763e-934">A rank build is a technical build that allows you toolearn about hello usefulness of your features.</span></span> <span data-ttu-id="2763e-935">Por lo general, en orden tooget Hola mejores resultados para un modelo de recomendación que implican características, debe tener Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2763e-935">Usually, in order tooget hello best result for a recommendation model involving features, you should take hello following steps:</span></span>

* <span data-ttu-id="2763e-936">Desencadenar una compilación rank (a menos que la puntuación de Hola de características es estable) y espere a que se obtendrá la puntuación de la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-936">Trigger a rank build (unless hello score of your features is stable) and wait till you get hello feature score.</span></span>
* <span data-ttu-id="2763e-937">Recuperar rango Hola de las funciones de llamada hello [obtener información de características](#101-get-features-info-for-last-rank-build) API.</span><span class="sxs-lookup"><span data-stu-id="2763e-937">Retrieve hello rank of your features by calling hello [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="2763e-938">Configurar una compilación de recomendación con hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-938">Configure a recommendation build with hello following parameters:</span></span>
  * <span data-ttu-id="2763e-939">`useFeatureInModel`-Establecer tooTrue.</span><span class="sxs-lookup"><span data-stu-id="2763e-939">`useFeatureInModel` - Set tooTrue.</span></span>
  * <span data-ttu-id="2763e-940">`ModelingFeatureList`-Set tooa-lista separados por comas de características con una puntuación de 2.0 o más (según la rangos toohello recuperado en el paso anterior de hello).</span><span class="sxs-lookup"><span data-stu-id="2763e-940">`ModelingFeatureList` - Set tooa comma-separated list of features with a score of 2.0 or more (according toohello ranks you retrieved in hello previous step).</span></span>
  * <span data-ttu-id="2763e-941">`AllowColdItemPlacement`-Establecer tooTrue.</span><span class="sxs-lookup"><span data-stu-id="2763e-941">`AllowColdItemPlacement` - Set tooTrue.</span></span>
  * <span data-ttu-id="2763e-942">Opcionalmente, puede establecer `EnableFeatureCorrelation` tooTrue y `ReasoningFeatureList` toohello lista de características que desea toouse para obtener una explicación (normalmente Hola misma lista de características se usa en una sublista o modelización).</span><span class="sxs-lookup"><span data-stu-id="2763e-942">Optionally you can set `EnableFeatureCorrelation` tooTrue and `ReasoningFeatureList` toohello list of features you want toouse for explanations (usually hello same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="2763e-943">Compilación de recomendación de Hola de desencadenador con hello configurado los parámetros.</span><span class="sxs-lookup"><span data-stu-id="2763e-943">Trigger hello recommendation build with hello configured parameters.</span></span>

<span data-ttu-id="2763e-944">Nota: Si no configura los parámetros (p. ej. de invocación de compilación de la recomendación de hello sin parámetros) o deshabilitar explícitamente de uso de Hola de características (p. ej. `UseFeatureInModel` establecer tooFalse), sistema Hola configurará parámetros relacionados con la característica de Hola toohello explica los valores anteriores en caso de que existe una compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="2763e-944">Note: If you do not configure any parameters (e.g. invoke hello recommendation build without parameters) or you do not explicitly disable hello usage of features (e.g. `UseFeatureInModel` set tooFalse), hello system will set up hello feature-related parameters toohello explained values above in case a rank build exists.</span></span>

<span data-ttu-id="2763e-945">No hay restricciones acerca de cómo ejecutar una compilación de rango y una recomendación generar de forma simultánea para hello mismo modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-945">There is no restriction on running a rank build and a recommendation build concurrently for hello same model.</span></span> <span data-ttu-id="2763e-946">No obstante, no se puede ejecutar dos compilaciones de hello mismo tipo en hello mismo modelo en paralelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-946">Nevertheless, you cannot run two builds of hello same type on hello same model in parallel.</span></span>

<span data-ttu-id="2763e-947">Una compilación FBT (con frecuencia se compra junto) es otro algoritmo de recomendación denominado a veces recomendador "conservador", que resulta conveniente para catálogos que no sean de naturaleza homogénea (homogéneo: libros, películas, algunos alimentos, moda; no homogéneo: equipos y dispositivos, entre dominios, gran diversidad).</span><span class="sxs-lookup"><span data-stu-id="2763e-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="2763e-948">Nota: si los archivos de uso que haya cargado hello contienen campo opcional Hola "tipo de evento", para FBT modelización sólo los eventos "Compra" se utilizará.</span><span class="sxs-lookup"><span data-stu-id="2763e-948">Note: if hello usage files that you uploaded contain hello optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="2763e-949">Si no se proporciona ningún tipo de evento, todos los eventos se considerarán de compra.</span><span class="sxs-lookup"><span data-stu-id="2763e-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="2763e-950">11.1 Parámetros de compilación</span><span class="sxs-lookup"><span data-stu-id="2763e-950">11.1 Build parameters</span></span>
<span data-ttu-id="2763e-951">Cada tipo de compilación puede configurarse a través de un conjunto de parámetros (se muestra a continuación).</span><span class="sxs-lookup"><span data-stu-id="2763e-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="2763e-952">Si no configura los parámetros de hello, sistema de hello automáticamente de atributo valores toohello parámetros según la información de toohello presente en el momento de hello desencadenar una compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-952">If you don't configure hello parameters, hello system will automatically attribute values toohello parameters according toohello information present at hello time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="2763e-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="2763e-953">11.1.1.</span></span> <span data-ttu-id="2763e-954">Condensador de uso</span><span class="sxs-lookup"><span data-stu-id="2763e-954">Usage condenser</span></span>
<span data-ttu-id="2763e-955">Los usuarios o elementos con pocos puntos de uso podrían contener más ruido de información.</span><span class="sxs-lookup"><span data-stu-id="2763e-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="2763e-956">sistema de Hello intente toopredict Hola un número mínimo de puntos de uso por toobe/elemento de usuario usadas en un modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-956">hello system attempts toopredict hello minimal number of usage points per user/item toobe used in a model.</span></span> <span data-ttu-id="2763e-957">Este número será dentro de intervalo de hello definido hello ItemCutoffLowerBound y los parámetros de ItemCutoffUpperBound elementos e intervalo de hello definida por hello UserCutOffLowerBound y parámetros de UserCutoffUpperBound para los usuarios de.</span><span class="sxs-lookup"><span data-stu-id="2763e-957">This number will be within hello range defined by hello ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and hello range defined by hello UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="2763e-958">efecto de condensador Hello en elementos o los usuarios puede reducirse mediante la configuración de al menos uno de hello correspondiente límites toozero.</span><span class="sxs-lookup"><span data-stu-id="2763e-958">hello condenser effect on items or users can be minimized by setting at least one of hello corresponding bounds toozero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="2763e-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-959">11.1.2.</span></span> <span data-ttu-id="2763e-960">Parámetros de compilación de rango</span><span class="sxs-lookup"><span data-stu-id="2763e-960">Rank build parameters</span></span>
<span data-ttu-id="2763e-961">a continuación de la tabla de Hello muestra los parámetros de compilación de Hola para una compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="2763e-961">hello table below depicts hello build parameters for a rank build.</span></span>

| <span data-ttu-id="2763e-962">Clave</span><span class="sxs-lookup"><span data-stu-id="2763e-962">Key</span></span> | <span data-ttu-id="2763e-963">Description</span><span class="sxs-lookup"><span data-stu-id="2763e-963">Description</span></span> | <span data-ttu-id="2763e-964">Tipo</span><span class="sxs-lookup"><span data-stu-id="2763e-964">Type</span></span> | <span data-ttu-id="2763e-965">Valor válido</span><span class="sxs-lookup"><span data-stu-id="2763e-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2763e-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="2763e-966">NumberOfModelIterations</span></span> |<span data-ttu-id="2763e-967">número de Hola de iteraciones que realiza el modelo de Hola se refleja en hello hello y tiempo de precisión del modelo de proceso general.</span><span class="sxs-lookup"><span data-stu-id="2763e-967">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="2763e-968">número mayor de Hola de Hello, obtendrá de conseguir una mayor precisión de hello, pero Hola proceso tardará más tiempo.</span><span class="sxs-lookup"><span data-stu-id="2763e-968">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="2763e-969">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-969">Integer</span></span> |<span data-ttu-id="2763e-970">10-50</span><span class="sxs-lookup"><span data-stu-id="2763e-970">10-50</span></span> |
| <span data-ttu-id="2763e-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="2763e-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="2763e-972">número de Hola de dimensiones se relaciona toohello número de modelo de hello 'features' intentará toofind dentro de los datos.</span><span class="sxs-lookup"><span data-stu-id="2763e-972">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="2763e-973">Aumentar el número de Hola de dimensiones le permitirá optimizar mejor de los resultados de hello en clústeres más pequeños.</span><span class="sxs-lookup"><span data-stu-id="2763e-973">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="2763e-974">Sin embargo, hay demasiadas dimensiones impedirá modelo Hola buscar las correlaciones entre los elementos.</span><span class="sxs-lookup"><span data-stu-id="2763e-974">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="2763e-975">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-975">Integer</span></span> |<span data-ttu-id="2763e-976">10-40</span><span class="sxs-lookup"><span data-stu-id="2763e-976">10-40</span></span> |
| <span data-ttu-id="2763e-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="2763e-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="2763e-978">Define el límite de hello elemento inferior para condensador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-978">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="2763e-979">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2763e-979">See usage condenser above.</span></span> |<span data-ttu-id="2763e-980">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-980">Integer</span></span> |<span data-ttu-id="2763e-981">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="2763e-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="2763e-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="2763e-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="2763e-983">Define el límite de hello elemento superior para condensador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-983">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="2763e-984">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2763e-984">See usage condenser above.</span></span> |<span data-ttu-id="2763e-985">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-985">Integer</span></span> |<span data-ttu-id="2763e-986">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="2763e-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="2763e-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="2763e-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="2763e-988">Define el límite de hello usuario inferior para condensador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-988">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="2763e-989">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2763e-989">See usage condenser above.</span></span> |<span data-ttu-id="2763e-990">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-990">Integer</span></span> |<span data-ttu-id="2763e-991">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="2763e-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="2763e-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="2763e-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="2763e-993">Define el límite de hello usuario superior para condensador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-993">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="2763e-994">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2763e-994">See usage condenser above.</span></span> |<span data-ttu-id="2763e-995">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-995">Integer</span></span> |<span data-ttu-id="2763e-996">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="2763e-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="2763e-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="2763e-997">11.1.3.</span></span> <span data-ttu-id="2763e-998">Parámetros de compilación de recomendación</span><span class="sxs-lookup"><span data-stu-id="2763e-998">Recommendation build parameters</span></span>
<span data-ttu-id="2763e-999">tabla de Hello siguiente describe los parámetros de compilación de Hola para compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="2763e-999">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="2763e-1000">Clave</span><span class="sxs-lookup"><span data-stu-id="2763e-1000">Key</span></span> | <span data-ttu-id="2763e-1001">Description</span><span class="sxs-lookup"><span data-stu-id="2763e-1001">Description</span></span> | <span data-ttu-id="2763e-1002">Tipo</span><span class="sxs-lookup"><span data-stu-id="2763e-1002">Type</span></span> | <span data-ttu-id="2763e-1003">Valor válido</span><span class="sxs-lookup"><span data-stu-id="2763e-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2763e-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="2763e-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="2763e-1005">número de Hola de iteraciones que realiza el modelo de Hola se refleja en hello hello y tiempo de precisión del modelo de proceso general.</span><span class="sxs-lookup"><span data-stu-id="2763e-1005">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="2763e-1006">número mayor de Hola de Hello, obtendrá de conseguir una mayor precisión de hello, pero Hola proceso tardará más tiempo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1006">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="2763e-1007">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1007">Integer</span></span> |<span data-ttu-id="2763e-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="2763e-1008">10-50</span></span> |
| <span data-ttu-id="2763e-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="2763e-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="2763e-1010">número de Hola de dimensiones se relaciona toohello número de modelo de hello 'features' intentará toofind dentro de los datos.</span><span class="sxs-lookup"><span data-stu-id="2763e-1010">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="2763e-1011">Aumentar el número de Hola de dimensiones le permitirá optimizar mejor de los resultados de hello en clústeres más pequeños.</span><span class="sxs-lookup"><span data-stu-id="2763e-1011">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="2763e-1012">Sin embargo, hay demasiadas dimensiones impedirá modelo Hola buscar las correlaciones entre los elementos.</span><span class="sxs-lookup"><span data-stu-id="2763e-1012">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="2763e-1013">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1013">Integer</span></span> |<span data-ttu-id="2763e-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="2763e-1014">10-40</span></span> |
| <span data-ttu-id="2763e-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="2763e-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="2763e-1016">Define el límite de hello elemento inferior para condensador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1016">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="2763e-1017">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1017">See usage condenser above.</span></span> |<span data-ttu-id="2763e-1018">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1018">Integer</span></span> |<span data-ttu-id="2763e-1019">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="2763e-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="2763e-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="2763e-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="2763e-1021">Define el límite de hello elemento superior para condensador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1021">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="2763e-1022">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1022">See usage condenser above.</span></span> |<span data-ttu-id="2763e-1023">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1023">Integer</span></span> |<span data-ttu-id="2763e-1024">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="2763e-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="2763e-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="2763e-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="2763e-1026">Define el límite de hello usuario inferior para condensador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1026">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="2763e-1027">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1027">See usage condenser above.</span></span> |<span data-ttu-id="2763e-1028">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1028">Integer</span></span> |<span data-ttu-id="2763e-1029">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="2763e-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="2763e-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="2763e-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="2763e-1031">Define el límite de hello usuario superior para condensador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1031">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="2763e-1032">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1032">See usage condenser above.</span></span> |<span data-ttu-id="2763e-1033">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1033">Integer</span></span> |<span data-ttu-id="2763e-1034">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="2763e-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="2763e-1035">Description</span><span class="sxs-lookup"><span data-stu-id="2763e-1035">Description</span></span> |<span data-ttu-id="2763e-1036">Descripción de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1036">Build description.</span></span> |<span data-ttu-id="2763e-1037">String</span><span class="sxs-lookup"><span data-stu-id="2763e-1037">String</span></span> |<span data-ttu-id="2763e-1038">Cualquier texto, máximo 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="2763e-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="2763e-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="2763e-1039">EnableModelingInsights</span></span> |<span data-ttu-id="2763e-1040">Le permite toocompute métricas en el modelo de recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1040">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="2763e-1041">Booleano</span><span class="sxs-lookup"><span data-stu-id="2763e-1041">Boolean</span></span> |<span data-ttu-id="2763e-1042">True/False</span><span class="sxs-lookup"><span data-stu-id="2763e-1042">True/False</span></span> |
| <span data-ttu-id="2763e-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="2763e-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="2763e-1044">Indica si se pueden utilizar características en el modelo de recomendación de orden tooenhance Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1044">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="2763e-1045">Booleano</span><span class="sxs-lookup"><span data-stu-id="2763e-1045">Boolean</span></span> |<span data-ttu-id="2763e-1046">True/False</span><span class="sxs-lookup"><span data-stu-id="2763e-1046">True/False</span></span> |
| <span data-ttu-id="2763e-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="2763e-1047">ModelingFeatureList</span></span> |<span data-ttu-id="2763e-1048">Lista separada por comas de toobe de nombres de característica utilizado en la compilación de recomendación de hello, en la recomendación de orden tooenhance Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1048">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="2763e-1049">String</span><span class="sxs-lookup"><span data-stu-id="2763e-1049">String</span></span> |<span data-ttu-id="2763e-1050">Nombres de las características, los caracteres de too512</span><span class="sxs-lookup"><span data-stu-id="2763e-1050">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="2763e-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="2763e-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="2763e-1052">Indica si la recomendación de hello también debería insertar elementos fríos a través de la similitud de características.</span><span class="sxs-lookup"><span data-stu-id="2763e-1052">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="2763e-1053">Booleano</span><span class="sxs-lookup"><span data-stu-id="2763e-1053">Boolean</span></span> |<span data-ttu-id="2763e-1054">True/False</span><span class="sxs-lookup"><span data-stu-id="2763e-1054">True/False</span></span> |
| <span data-ttu-id="2763e-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="2763e-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="2763e-1056">Indica si se pueden utilizar características en el razonamiento.</span><span class="sxs-lookup"><span data-stu-id="2763e-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="2763e-1057">Booleano</span><span class="sxs-lookup"><span data-stu-id="2763e-1057">Boolean</span></span> |<span data-ttu-id="2763e-1058">True/False</span><span class="sxs-lookup"><span data-stu-id="2763e-1058">True/False</span></span> |
| <span data-ttu-id="2763e-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="2763e-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="2763e-1060">Lista separada por comas de toobe de nombres de función permiten razonamiento frases (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="2763e-1060">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="2763e-1061">String</span><span class="sxs-lookup"><span data-stu-id="2763e-1061">String</span></span> |<span data-ttu-id="2763e-1062">Nombres de las características, los caracteres de too512</span><span class="sxs-lookup"><span data-stu-id="2763e-1062">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="2763e-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="2763e-1063">EnableU2I</span></span> |<span data-ttu-id="2763e-1064">Permitir conocido como recomendación de hello personalizada</span><span class="sxs-lookup"><span data-stu-id="2763e-1064">Allow hello personalized recommendation a.k.a.</span></span> <span data-ttu-id="2763e-1065">U2I (recomendaciones de tooitem de usuario).</span><span class="sxs-lookup"><span data-stu-id="2763e-1065">U2I (user tooitem recommendations).</span></span> |<span data-ttu-id="2763e-1066">Booleano</span><span class="sxs-lookup"><span data-stu-id="2763e-1066">Boolean</span></span> |<span data-ttu-id="2763e-1067">True/False (true de forma predeterminada)</span><span class="sxs-lookup"><span data-stu-id="2763e-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="2763e-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="2763e-1068">11.1.4.</span></span> <span data-ttu-id="2763e-1069">Parámetros de compilación FBT</span><span class="sxs-lookup"><span data-stu-id="2763e-1069">FBT build parameters</span></span>
<span data-ttu-id="2763e-1070">tabla de Hello siguiente describe los parámetros de compilación de Hola para compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1070">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="2763e-1071">Clave</span><span class="sxs-lookup"><span data-stu-id="2763e-1071">Key</span></span> | <span data-ttu-id="2763e-1072">Description</span><span class="sxs-lookup"><span data-stu-id="2763e-1072">Description</span></span> | <span data-ttu-id="2763e-1073">Tipo</span><span class="sxs-lookup"><span data-stu-id="2763e-1073">Type</span></span> | <span data-ttu-id="2763e-1074">Valor válido (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="2763e-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2763e-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="2763e-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="2763e-1076">Cómo es el modelo conservador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1076">How conservative hello model is.</span></span> <span data-ttu-id="2763e-1077">Número de repeticiones coadministradores de toobe de elementos que se consideran para el modelado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1077">Number of co-occurrences of items toobe considered for modeling.</span></span> |<span data-ttu-id="2763e-1078">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1078">Integer</span></span> |<span data-ttu-id="2763e-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="2763e-1079">3-50 (6)</span></span> |
| <span data-ttu-id="2763e-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="2763e-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="2763e-1081">Límites Hola número de elementos de un conjunto frecuente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1081">Bounds hello number of items in a frequent set.</span></span> |<span data-ttu-id="2763e-1082">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1082">Integer</span></span> |<span data-ttu-id="2763e-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="2763e-1083">2-3 (2)</span></span> |
| <span data-ttu-id="2763e-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="2763e-1084">FbtMinimalScore</span></span> |<span data-ttu-id="2763e-1085">Puntuación mínima que frecuentes devuelve un conjunto debe haber en toobe orden incluido en hello da como resultado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1085">Minimal score that a frequent set should have in order toobe included in hello returned results.</span></span> <span data-ttu-id="2763e-1086">Hola superior Hola mejor.</span><span class="sxs-lookup"><span data-stu-id="2763e-1086">hello higher hello better.</span></span> |<span data-ttu-id="2763e-1087">Double</span><span class="sxs-lookup"><span data-stu-id="2763e-1087">Double</span></span> |<span data-ttu-id="2763e-1088">0 y superior (0)</span><span class="sxs-lookup"><span data-stu-id="2763e-1088">0 and above (0)</span></span> |
| <span data-ttu-id="2763e-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="2763e-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="2763e-1090">Define Hola similitud función toobe utilizado por compilación Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1090">Defines hello similarity function toobe used by hello build.</span></span> <span data-ttu-id="2763e-1091">Elevación favorece serendipity, aparición coadministradores favorece previsibilidad y Jaccard es un compromiso entre dos Hola "nice".</span><span class="sxs-lookup"><span data-stu-id="2763e-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between hello two.</span></span> |<span data-ttu-id="2763e-1092">String</span><span class="sxs-lookup"><span data-stu-id="2763e-1092">String</span></span> |<span data-ttu-id="2763e-1093">cooccurrence, lift, jaccard (lift)</span><span class="sxs-lookup"><span data-stu-id="2763e-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="2763e-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-1094">11.2.</span></span> <span data-ttu-id="2763e-1095">Desencadenar una compilación de recomendación</span><span class="sxs-lookup"><span data-stu-id="2763e-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="2763e-1096">De forma predeterminada, esta API desencadenará una compilación de modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="2763e-1097">tootrigger un rango de compilación (en las características de tooscore de pedido), debe usarse la variante de API de generación de hello con el parámetro de tipo de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1097">tootrigger a rank build (in order tooscore  features), hello build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="2763e-1098">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1098">HTTP Method</span></span> | <span data-ttu-id="2763e-1099">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1100">POST</span><span class="sxs-lookup"><span data-stu-id="2763e-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1101">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="2763e-1102">ENCABEZADO</span><span class="sxs-lookup"><span data-stu-id="2763e-1102">HEADER</span></span> |<span data-ttu-id="2763e-1103">`"Content-Type", "text/xml"` (Si se envía el cuerpo de la solicitud)</span><span class="sxs-lookup"><span data-stu-id="2763e-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="2763e-1104">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1104">Parameter Name</span></span> | <span data-ttu-id="2763e-1105">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1106">modelId</span></span> |<span data-ttu-id="2763e-1107">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1107">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="2763e-1108">userDescription</span></span> |<span data-ttu-id="2763e-1109">Identificador textual del catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1109">Textual identifier of hello catalog.</span></span> <span data-ttu-id="2763e-1110">Tenga en cuenta que si usa espacios debe codificarlo en su lugar con un 20 %.</span><span class="sxs-lookup"><span data-stu-id="2763e-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="2763e-1111">Vea el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="2763e-1111">See example above.</span></span><br><span data-ttu-id="2763e-1112">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="2763e-1112">Max length: 50</span></span> |
| <span data-ttu-id="2763e-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1113">apiVersion</span></span> |<span data-ttu-id="2763e-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-1115">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-1115">Request Body</span></span> |<span data-ttu-id="2763e-1116">Si se deja vacío, a continuación, compilación Hola se ejecutarán con parámetros de compilación de hello predeterminados.</span><span class="sxs-lookup"><span data-stu-id="2763e-1116">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="2763e-1117">Si desea que los parámetros de compilación de hello tooset, enviar parámetros de hello como XML en el cuerpo de hello como en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1117">If you want tooset hello build parameters, send hello parameters as XML into hello body as in hello following sample.</span></span> <span data-ttu-id="2763e-1118">(Consulte la sección de Hola "parámetros de compilación" para obtener una explicación de los parámetros de Hola.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="2763e-1118">(See hello "Build parameters" section for an explanation of hello parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="2763e-1119">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-1119">**Response**:</span></span>

<span data-ttu-id="2763e-1120">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1121">Se trata de una API asincrónica.</span><span class="sxs-lookup"><span data-stu-id="2763e-1121">This is an asynchronous API.</span></span> <span data-ttu-id="2763e-1122">Obtendrá un Id. de compilación como respuesta.</span><span class="sxs-lookup"><span data-stu-id="2763e-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="2763e-1123">tooknow cuando ha finalizado la generación de hello, debe llamar a la API de "Obtener compilaciones estado de un modelo de" hello y busque este Id. de compilación en la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1123">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="2763e-1124">Tenga en cuenta que una compilación puede tardar desde toohours minutos según el tamaño de Hola de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1124">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="2763e-1125">No se puede consumir recomendaciones hasta Hola crear extremos.</span><span class="sxs-lookup"><span data-stu-id="2763e-1125">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="2763e-1126">Estado de compilación válido:</span><span class="sxs-lookup"><span data-stu-id="2763e-1126">Valid build status:</span></span>

* <span data-ttu-id="2763e-1127">Crear: se ha creado la solicitud de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="2763e-1128">En cola: la solicitud de compilación se ha enviado y puesto en cola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="2763e-1129">Compilando: la compilación está en curso.</span><span class="sxs-lookup"><span data-stu-id="2763e-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="2763e-1130">Correcto: la compilación finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="2763e-1131">Error: la compilación finalizó con un error.</span><span class="sxs-lookup"><span data-stu-id="2763e-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="2763e-1132">Cancelada: se canceló la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="2763e-1133">Cancelar: se ha enviado una solicitud de cancelación para compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1133">Cancelling - A cancel request for hello build was sent.</span></span>

<span data-ttu-id="2763e-1134">Tenga en cuenta esa compilación Hola que identificador puede encontrarse en hello siguiendo la ruta de acceso:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="2763e-1134">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="2763e-1135">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-1135">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="2763e-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="2763e-1136">11.3.</span></span> <span data-ttu-id="2763e-1137">Desencadenar compilación (recomendación, rango o FBT)</span><span class="sxs-lookup"><span data-stu-id="2763e-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="2763e-1138">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1138">HTTP Method</span></span> | <span data-ttu-id="2763e-1139">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1140">POST</span><span class="sxs-lookup"><span data-stu-id="2763e-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1141">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="2763e-1142">ENCABEZADO</span><span class="sxs-lookup"><span data-stu-id="2763e-1142">HEADER</span></span> |<span data-ttu-id="2763e-1143">`"Content-Type", "text/xml"` (Si se envía el cuerpo de la solicitud)</span><span class="sxs-lookup"><span data-stu-id="2763e-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="2763e-1144">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1144">Parameter Name</span></span> | <span data-ttu-id="2763e-1145">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1146">modelId</span></span> |<span data-ttu-id="2763e-1147">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1147">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="2763e-1148">userDescription</span></span> |<span data-ttu-id="2763e-1149">Identificador textual del catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1149">Textual identifier of hello catalog.</span></span> <span data-ttu-id="2763e-1150">Tenga en cuenta que si usa espacios debe codificarlo en su lugar con un 20 %.</span><span class="sxs-lookup"><span data-stu-id="2763e-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="2763e-1151">Vea el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="2763e-1151">See example above.</span></span><br><span data-ttu-id="2763e-1152">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="2763e-1152">Max length: 50</span></span> |
| <span data-ttu-id="2763e-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="2763e-1153">buildType</span></span> |<span data-ttu-id="2763e-1154">Tipo de hello compilación tooinvoke:</span><span class="sxs-lookup"><span data-stu-id="2763e-1154">Type of hello build tooinvoke:</span></span> <br/> <span data-ttu-id="2763e-1155">"Recomendación" para compilación de recomendación</span><span class="sxs-lookup"><span data-stu-id="2763e-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="2763e-1156">-"Categoría" para una compilación de rango</span><span class="sxs-lookup"><span data-stu-id="2763e-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="2763e-1157">- 'Fbt' para compilación FBT</span><span class="sxs-lookup"><span data-stu-id="2763e-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="2763e-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1158">apiVersion</span></span> |<span data-ttu-id="2763e-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-1160">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-1160">Request Body</span></span> |<span data-ttu-id="2763e-1161">Si se deja vacío, a continuación, compilación Hola se ejecutarán con parámetros de compilación de hello predeterminados.</span><span class="sxs-lookup"><span data-stu-id="2763e-1161">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="2763e-1162">Si desea que los parámetros de compilación tooset, enviarlos como XML en el cuerpo de hello como en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1162">If you want tooset build parameters, send them as XML into hello body like in hello following sample.</span></span> <span data-ttu-id="2763e-1163">(Consulte la sección de "parámetros de compilación" hello para una explicación y una lista completa de parámetros de Hola.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="2763e-1163">(See hello "Build parameters" section for an explanation and full list of hello parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="2763e-1164">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-1164">**Response**:</span></span>

<span data-ttu-id="2763e-1165">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1166">Se trata de una API asincrónica.</span><span class="sxs-lookup"><span data-stu-id="2763e-1166">This is an asynchronous API.</span></span> <span data-ttu-id="2763e-1167">Obtendrá un Id. de compilación como respuesta.</span><span class="sxs-lookup"><span data-stu-id="2763e-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="2763e-1168">tooknow cuando ha finalizado la generación de hello, debe llamar a la API de "Obtener compilaciones estado de un modelo de" hello y busque este Id. de compilación en la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1168">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="2763e-1169">Tenga en cuenta que una compilación puede tardar desde toohours minutos según el tamaño de Hola de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1169">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="2763e-1170">No se puede consumir recomendaciones hasta Hola crear extremos.</span><span class="sxs-lookup"><span data-stu-id="2763e-1170">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="2763e-1171">Estado de compilación válido:</span><span class="sxs-lookup"><span data-stu-id="2763e-1171">Valid build status:</span></span>

* <span data-ttu-id="2763e-1172">Crear: se creó el modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1172">Create - Model was created.</span></span>
* <span data-ttu-id="2763e-1173">En cola: se desencadenó la compilación del modelo y está en la cola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="2763e-1174">Compilando: el modelo se está compilando.</span><span class="sxs-lookup"><span data-stu-id="2763e-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="2763e-1175">Correcto: la compilación finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="2763e-1176">Error: la compilación finalizó con un error.</span><span class="sxs-lookup"><span data-stu-id="2763e-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="2763e-1177">Cancelada: se canceló la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="2763e-1178">Cancelando: la compilación se está cancelando.</span><span class="sxs-lookup"><span data-stu-id="2763e-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="2763e-1179">Tenga en cuenta esa compilación Hola que identificador puede encontrarse en hello siguiendo la ruta de acceso:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="2763e-1179">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="2763e-1180">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-1180">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="2763e-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="2763e-1181">11.4.</span></span> <span data-ttu-id="2763e-1182">Obtener el estado de compilación de un modelo</span><span class="sxs-lookup"><span data-stu-id="2763e-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="2763e-1183">Recupera las compilaciones y su estado para un modelo especificado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="2763e-1184">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1184">HTTP Method</span></span> | <span data-ttu-id="2763e-1185">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1186">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1187">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1188">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1188">Parameter Name</span></span> | <span data-ttu-id="2763e-1189">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1190">modelId</span></span> |<span data-ttu-id="2763e-1191">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1191">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="2763e-1192">onlyLastBuild</span></span> |<span data-ttu-id="2763e-1193">Indica si tooreturn Hola a todos crear historial de modelo de Hola o solo de estado de Hola de compilación más reciente de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1193">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build</span></span> |
| <span data-ttu-id="2763e-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1194">apiVersion</span></span> |<span data-ttu-id="2763e-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1195">1.0</span></span> |

<span data-ttu-id="2763e-1196">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-1196">**Response**:</span></span>

<span data-ttu-id="2763e-1197">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1198">respuesta de Hello incluye una entrada por cada compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1198">hello response includes one entry per build.</span></span> <span data-ttu-id="2763e-1199">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-1199">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-1200">`feed/entry/content/properties/UserName`-Nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1200">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="2763e-1201">`feed/entry/content/properties/ModelName`-Nombre del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1201">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="2763e-1202">`feed/entry/content/properties/ModelId` : identificador único de modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="2763e-1203">`feed/entry/content/properties/IsDeployed`-Si se implementa compilación hello (conocido como)</span><span class="sxs-lookup"><span data-stu-id="2763e-1203">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="2763e-1204">compilación activa).</span><span class="sxs-lookup"><span data-stu-id="2763e-1204">active build).</span></span>
* <span data-ttu-id="2763e-1205">`feed/entry/content/properties/BuildId` : identificador único de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="2763e-1206">`feed/entry/content/properties/BuildType`-Tipo de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1206">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="2763e-1207">`feed/entry/content/properties/Status` : estado de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="2763e-1208">Puede ser uno de los siguientes de hello: Error, creación, en cola, cancelando, cancelado, correcto.</span><span class="sxs-lookup"><span data-stu-id="2763e-1208">Can be one of hello following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="2763e-1209">`feed/entry/content/properties/StatusMessage`-Mensaje de estado detallado (se aplica solo toospecific estados).</span><span class="sxs-lookup"><span data-stu-id="2763e-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="2763e-1210">`feed/entry/content/properties/Progress` : progreso de la compilación (%).</span><span class="sxs-lookup"><span data-stu-id="2763e-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="2763e-1211">`feed/entry/content/properties/StartTime` : hora de inicio de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="2763e-1212">`feed/entry/content/properties/EndTime` : hora de finalización de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="2763e-1213">`feed/entry/content/properties/ExecutionTime` : duración de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="2763e-1214">`feed/entry/content/properties/ProgressStep`-Los detalles acerca de la fase actual de Hola de una compilación en curso.</span><span class="sxs-lookup"><span data-stu-id="2763e-1214">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="2763e-1215">Estado de compilación válido:</span><span class="sxs-lookup"><span data-stu-id="2763e-1215">Valid build status:</span></span>

* <span data-ttu-id="2763e-1216">Creado: se creó la entrada de solicitud de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="2763e-1217">En cola: la solicitud de compilación se ha desencadenado y puesto en cola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="2763e-1218">Compilando: la compilación está en curso.</span><span class="sxs-lookup"><span data-stu-id="2763e-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="2763e-1219">Correcto: la compilación finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="2763e-1220">Error: la compilación finalizó con un error.</span><span class="sxs-lookup"><span data-stu-id="2763e-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="2763e-1221">Cancelada: se canceló la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="2763e-1222">Cancelando: la compilación se está cancelando.</span><span class="sxs-lookup"><span data-stu-id="2763e-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="2763e-1223">Valores válidos para el tipo de compilación:</span><span class="sxs-lookup"><span data-stu-id="2763e-1223">Valid values for build type:</span></span>

* <span data-ttu-id="2763e-1224">Rango: compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="2763e-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="2763e-1225">Recomendación: compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="2763e-1226">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-1226">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a><span data-ttu-id="2763e-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="2763e-1227">11.5.</span></span> <span data-ttu-id="2763e-1228">Obtener estado de compilación</span><span class="sxs-lookup"><span data-stu-id="2763e-1228">Get Builds Status</span></span>
<span data-ttu-id="2763e-1229">Recupera los estados de compilación de todos los modelos de un usuario</span><span class="sxs-lookup"><span data-stu-id="2763e-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="2763e-1230">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1230">HTTP Method</span></span> | <span data-ttu-id="2763e-1231">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1232">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1233">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1234">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1234">Parameter Name</span></span> | <span data-ttu-id="2763e-1235">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="2763e-1236">onlyLastBuild</span></span> |<span data-ttu-id="2763e-1237">Indica si tooreturn Hola a todos crear historial de modelo de Hola o solo de estado de Hola de compilación más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1237">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="2763e-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1238">apiVersion</span></span> |<span data-ttu-id="2763e-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1239">1.0</span></span> |

<span data-ttu-id="2763e-1240">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-1240">**Response**:</span></span>

<span data-ttu-id="2763e-1241">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1242">respuesta de Hello incluye una entrada por cada compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1242">hello response includes one entry per build.</span></span> <span data-ttu-id="2763e-1243">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-1243">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-1244">`feed/entry/content/properties/UserName`-Nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1244">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="2763e-1245">`feed/entry/content/properties/ModelName`-Nombre del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1245">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="2763e-1246">`feed/entry/content/properties/ModelId` : identificador único de modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="2763e-1247">`feed/entry/content/properties/IsDeployed`-Si está implementada la compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1247">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed.</span></span>
* <span data-ttu-id="2763e-1248">`feed/entry/content/properties/BuildId` : identificador único de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="2763e-1249">`feed/entry/content/properties/BuildType`-Tipo de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1249">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="2763e-1250">`feed/entry/content/properties/Status` : estado de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="2763e-1251">Puede ser uno de los siguientes de hello: Error, creación, en cola, cancelado, cancelando, correcto.</span><span class="sxs-lookup"><span data-stu-id="2763e-1251">Can be one of hello following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="2763e-1252">`feed/entry/content/properties/StatusMessage`-Mensaje de estado detallado (se aplica solo toospecific estados).</span><span class="sxs-lookup"><span data-stu-id="2763e-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="2763e-1253">`feed/entry/content/properties/Progress` : progreso de la compilación (%).</span><span class="sxs-lookup"><span data-stu-id="2763e-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="2763e-1254">`feed/entry/content/properties/StartTime` : hora de inicio de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="2763e-1255">`feed/entry/content/properties/EndTime` : hora de finalización de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="2763e-1256">`feed/entry/content/properties/ExecutionTime` : duración de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="2763e-1257">`feed/entry/content/properties/ProgressStep`-Los detalles acerca de la fase actual de Hola de una compilación en curso.</span><span class="sxs-lookup"><span data-stu-id="2763e-1257">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="2763e-1258">Estado de compilación válido:</span><span class="sxs-lookup"><span data-stu-id="2763e-1258">Valid build status:</span></span>

* <span data-ttu-id="2763e-1259">Creado: se creó la entrada de solicitud de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="2763e-1260">En cola: la solicitud de compilación se ha desencadenado y puesto en cola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="2763e-1261">Compilando: la compilación está en curso.</span><span class="sxs-lookup"><span data-stu-id="2763e-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="2763e-1262">Correcto: la compilación finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="2763e-1263">Error: la compilación finalizó con un error.</span><span class="sxs-lookup"><span data-stu-id="2763e-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="2763e-1264">Cancelada: se canceló la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="2763e-1265">Cancelando: la compilación se está cancelando.</span><span class="sxs-lookup"><span data-stu-id="2763e-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="2763e-1266">Valores válidos para el tipo de compilación:</span><span class="sxs-lookup"><span data-stu-id="2763e-1266">Valid values for build type:</span></span>

* <span data-ttu-id="2763e-1267">Rango: compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="2763e-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="2763e-1268">Recomendación: compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="2763e-1269">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-1269">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a><span data-ttu-id="2763e-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="2763e-1270">11.6.</span></span> <span data-ttu-id="2763e-1271">Eliminar compilación</span><span class="sxs-lookup"><span data-stu-id="2763e-1271">Delete Build</span></span>
<span data-ttu-id="2763e-1272">Elimina una compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1272">Deletes a build.</span></span>

<span data-ttu-id="2763e-1273">NOTA: </span><span class="sxs-lookup"><span data-stu-id="2763e-1273">NOTE:</span></span> <br><span data-ttu-id="2763e-1274">no se puede eliminar una compilación activa.</span><span class="sxs-lookup"><span data-stu-id="2763e-1274">You cannot delete an active build.</span></span> <span data-ttu-id="2763e-1275">Hola modelo debe estar actualizado tooa diferentes active compilación antes de eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1275">hello model should be updated tooa different active build before you delete it.</span></span><br><span data-ttu-id="2763e-1276">No puede eliminar una compilación en curso.</span><span class="sxs-lookup"><span data-stu-id="2763e-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="2763e-1277">Debe cancelar compilación hello en primer lugar mediante una llamada a <strong>Cancelar compilación</strong>.</span><span class="sxs-lookup"><span data-stu-id="2763e-1277">You should cancel hello build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="2763e-1278">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1278">HTTP Method</span></span> | <span data-ttu-id="2763e-1279">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1280">DELETE</span><span class="sxs-lookup"><span data-stu-id="2763e-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1281">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1282">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1282">Parameter Name</span></span> | <span data-ttu-id="2763e-1283">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="2763e-1284">buildId</span></span> |<span data-ttu-id="2763e-1285">Identificador único de la compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1285">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="2763e-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1286">apiVersion</span></span> |<span data-ttu-id="2763e-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1287">1.0</span></span> |

<span data-ttu-id="2763e-1288">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1288">**Response:**</span></span>

<span data-ttu-id="2763e-1289">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="2763e-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="2763e-1290">11.7.</span></span> <span data-ttu-id="2763e-1291">Cancelar compilación</span><span class="sxs-lookup"><span data-stu-id="2763e-1291">Cancel Build</span></span>
<span data-ttu-id="2763e-1292">Cancela una compilación que se encuentra en estado Building.</span><span class="sxs-lookup"><span data-stu-id="2763e-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="2763e-1293">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1293">HTTP Method</span></span> | <span data-ttu-id="2763e-1294">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="2763e-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1296">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1297">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1297">Parameter Name</span></span> | <span data-ttu-id="2763e-1298">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="2763e-1299">buildId</span></span> |<span data-ttu-id="2763e-1300">Identificador único de la compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1300">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="2763e-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1301">apiVersion</span></span> |<span data-ttu-id="2763e-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1302">1.0</span></span> |

<span data-ttu-id="2763e-1303">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1303">**Response:**</span></span>

<span data-ttu-id="2763e-1304">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="2763e-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="2763e-1305">11.8.</span></span> <span data-ttu-id="2763e-1306">Obtener parámetros de compilación</span><span class="sxs-lookup"><span data-stu-id="2763e-1306">Get Build Parameters</span></span>
<span data-ttu-id="2763e-1307">Recupera parámetros de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="2763e-1308">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1308">HTTP Method</span></span> | <span data-ttu-id="2763e-1309">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1310">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1311">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1312">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1312">Parameter Name</span></span> | <span data-ttu-id="2763e-1313">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="2763e-1314">buildId</span></span> |<span data-ttu-id="2763e-1315">Identificador único de la compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1315">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="2763e-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1316">apiVersion</span></span> |<span data-ttu-id="2763e-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1317">1.0</span></span> |

<span data-ttu-id="2763e-1318">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1318">**Response:**</span></span>

<span data-ttu-id="2763e-1319">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1320">Esta API devuelve una colección de elementos de clave y valor.</span><span class="sxs-lookup"><span data-stu-id="2763e-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="2763e-1321">Cada elemento representa un parámetro y su valor:</span><span class="sxs-lookup"><span data-stu-id="2763e-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="2763e-1322">`feed/entry/content/properties/Key` : nombre del parámetro de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="2763e-1323">`feed/entry/content/properties/Value` : valor del parámetro de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="2763e-1324">a continuación de la tabla de Hello muestra valor Hola que representa cada clave.</span><span class="sxs-lookup"><span data-stu-id="2763e-1324">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="2763e-1325">Clave</span><span class="sxs-lookup"><span data-stu-id="2763e-1325">Key</span></span> | <span data-ttu-id="2763e-1326">Description</span><span class="sxs-lookup"><span data-stu-id="2763e-1326">Description</span></span> | <span data-ttu-id="2763e-1327">Tipo</span><span class="sxs-lookup"><span data-stu-id="2763e-1327">Type</span></span> | <span data-ttu-id="2763e-1328">Valor válido</span><span class="sxs-lookup"><span data-stu-id="2763e-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2763e-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="2763e-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="2763e-1330">número de Hola de iteraciones que realiza el modelo de Hola se refleja en hello hello y tiempo de precisión del modelo de proceso general.</span><span class="sxs-lookup"><span data-stu-id="2763e-1330">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="2763e-1331">número mayor de Hola de Hello, obtendrá de conseguir una mayor precisión de hello, pero Hola proceso tardará más tiempo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1331">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="2763e-1332">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1332">Integer</span></span> |<span data-ttu-id="2763e-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="2763e-1333">10-50</span></span> |
| <span data-ttu-id="2763e-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="2763e-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="2763e-1335">número de Hola de dimensiones se relaciona toohello número de modelo de hello 'features' intentará toofind dentro de los datos.</span><span class="sxs-lookup"><span data-stu-id="2763e-1335">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="2763e-1336">Aumentar el número de Hola de dimensiones le permitirá optimizar mejor de los resultados de hello en clústeres más pequeños.</span><span class="sxs-lookup"><span data-stu-id="2763e-1336">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="2763e-1337">Sin embargo, hay demasiadas dimensiones impedirá modelo Hola buscar las correlaciones entre los elementos.</span><span class="sxs-lookup"><span data-stu-id="2763e-1337">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="2763e-1338">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1338">Integer</span></span> |<span data-ttu-id="2763e-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="2763e-1339">10-40</span></span> |
| <span data-ttu-id="2763e-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="2763e-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="2763e-1341">Define el límite de hello elemento inferior para condensador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1341">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="2763e-1342">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1342">See usage condenser above.</span></span> |<span data-ttu-id="2763e-1343">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1343">Integer</span></span> |<span data-ttu-id="2763e-1344">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="2763e-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="2763e-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="2763e-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="2763e-1346">Define el límite de hello elemento superior para condensador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1346">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="2763e-1347">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1347">See usage condenser above.</span></span> |<span data-ttu-id="2763e-1348">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1348">Integer</span></span> |<span data-ttu-id="2763e-1349">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="2763e-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="2763e-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="2763e-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="2763e-1351">Define el límite de hello usuario inferior para condensador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1351">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="2763e-1352">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1352">See usage condenser above.</span></span> |<span data-ttu-id="2763e-1353">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1353">Integer</span></span> |<span data-ttu-id="2763e-1354">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="2763e-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="2763e-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="2763e-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="2763e-1356">Define el límite de hello usuario superior para condensador Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1356">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="2763e-1357">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2763e-1357">See usage condenser above.</span></span> |<span data-ttu-id="2763e-1358">Entero</span><span class="sxs-lookup"><span data-stu-id="2763e-1358">Integer</span></span> |<span data-ttu-id="2763e-1359">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="2763e-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="2763e-1360">Description</span><span class="sxs-lookup"><span data-stu-id="2763e-1360">Description</span></span> |<span data-ttu-id="2763e-1361">Descripción de la compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1361">Build description.</span></span> |<span data-ttu-id="2763e-1362">String</span><span class="sxs-lookup"><span data-stu-id="2763e-1362">String</span></span> |<span data-ttu-id="2763e-1363">Cualquier texto, máximo 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="2763e-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="2763e-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="2763e-1364">EnableModelingInsights</span></span> |<span data-ttu-id="2763e-1365">Le permite toocompute métricas en el modelo de recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1365">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="2763e-1366">Booleano</span><span class="sxs-lookup"><span data-stu-id="2763e-1366">Boolean</span></span> |<span data-ttu-id="2763e-1367">True/False</span><span class="sxs-lookup"><span data-stu-id="2763e-1367">True/False</span></span> |
| <span data-ttu-id="2763e-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="2763e-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="2763e-1369">Indica si se pueden utilizar características en el modelo de recomendación de orden tooenhance Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1369">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="2763e-1370">Booleano</span><span class="sxs-lookup"><span data-stu-id="2763e-1370">Boolean</span></span> |<span data-ttu-id="2763e-1371">True/False</span><span class="sxs-lookup"><span data-stu-id="2763e-1371">True/False</span></span> |
| <span data-ttu-id="2763e-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="2763e-1372">ModelingFeatureList</span></span> |<span data-ttu-id="2763e-1373">Lista separada por comas de toobe de nombres de característica utilizado en la compilación de recomendación de hello, en la recomendación de orden tooenhance Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1373">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="2763e-1374">String</span><span class="sxs-lookup"><span data-stu-id="2763e-1374">String</span></span> |<span data-ttu-id="2763e-1375">Nombres de las características, los caracteres de too512</span><span class="sxs-lookup"><span data-stu-id="2763e-1375">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="2763e-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="2763e-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="2763e-1377">Indica si la recomendación de hello también debería insertar elementos fríos a través de la similitud de características.</span><span class="sxs-lookup"><span data-stu-id="2763e-1377">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="2763e-1378">Booleano</span><span class="sxs-lookup"><span data-stu-id="2763e-1378">Boolean</span></span> |<span data-ttu-id="2763e-1379">True/False</span><span class="sxs-lookup"><span data-stu-id="2763e-1379">True/False</span></span> |
| <span data-ttu-id="2763e-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="2763e-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="2763e-1381">Indica si se pueden utilizar características en el razonamiento.</span><span class="sxs-lookup"><span data-stu-id="2763e-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="2763e-1382">Booleano</span><span class="sxs-lookup"><span data-stu-id="2763e-1382">Boolean</span></span> |<span data-ttu-id="2763e-1383">True/False</span><span class="sxs-lookup"><span data-stu-id="2763e-1383">True/False</span></span> |
| <span data-ttu-id="2763e-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="2763e-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="2763e-1385">Lista separada por comas de toobe de nombres de función permiten razonamiento frases (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="2763e-1385">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="2763e-1386">String</span><span class="sxs-lookup"><span data-stu-id="2763e-1386">String</span></span> |<span data-ttu-id="2763e-1387">Nombres de las características, los caracteres de too512</span><span class="sxs-lookup"><span data-stu-id="2763e-1387">Feature names, up too512 chars</span></span> |

<span data-ttu-id="2763e-1388">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-1388">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a><span data-ttu-id="2763e-1389">12. Recomendación</span><span class="sxs-lookup"><span data-stu-id="2763e-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="2763e-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="2763e-1390">12.1.</span></span> <span data-ttu-id="2763e-1391">Obtención de recomendaciones de elemento (para la compilación activa)</span><span class="sxs-lookup"><span data-stu-id="2763e-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="2763e-1392">Obtener recomendaciones de compilación activa de Hola de tipo "Recomendación" o "Fbt" basado en una lista de elementos de valores de inicialización (entrada).</span><span class="sxs-lookup"><span data-stu-id="2763e-1392">Get recommendations of hello active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="2763e-1393">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1393">HTTP Method</span></span> | <span data-ttu-id="2763e-1394">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1395">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1396">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1397">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1397">Parameter Name</span></span> | <span data-ttu-id="2763e-1398">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1399">modelId</span></span> |<span data-ttu-id="2763e-1400">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1400">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="2763e-1401">itemIds</span></span> |<span data-ttu-id="2763e-1402">Lista separada por comas de hello elementos toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="2763e-1402">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="2763e-1403">Si compilación activa hello es de tipo FBT, a continuación, puede enviar un único elemento.</span><span class="sxs-lookup"><span data-stu-id="2763e-1403">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="2763e-1404">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="2763e-1404">Max length: 1024</span></span> |
| <span data-ttu-id="2763e-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="2763e-1405">numberOfResults</span></span> |<span data-ttu-id="2763e-1406">Número de resultados obligatorios </span><span class="sxs-lookup"><span data-stu-id="2763e-1406">Number of required results</span></span> <br> <span data-ttu-id="2763e-1407">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="2763e-1407">Max: 150</span></span> |
| <span data-ttu-id="2763e-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="2763e-1408">includeMetatadata</span></span> |<span data-ttu-id="2763e-1409">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="2763e-1409">Future use, always false</span></span> |
| <span data-ttu-id="2763e-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1410">apiVersion</span></span> |<span data-ttu-id="2763e-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1411">1.0</span></span> |

<span data-ttu-id="2763e-1412">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1412">**Response:**</span></span>

<span data-ttu-id="2763e-1413">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1414">respuesta de Hello incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1414">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="2763e-1415">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-1415">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-1416">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="2763e-1417">`Feed\entry\content\properties\Name`-Nombre del elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1417">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="2763e-1418">`Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="2763e-1418">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="2763e-1419">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="2763e-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="2763e-1420">respuesta de ejemplo de Hola siguiente incluye 10 elementos recomendados.</span><span class="sxs-lookup"><span data-stu-id="2763e-1420">hello example response below includes 10 recommended items.</span></span>

<span data-ttu-id="2763e-1421">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-1421">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="2763e-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-1422">12.2.</span></span> <span data-ttu-id="2763e-1423">Obtención de recomendaciones de elemento (de una compilación concreta)</span><span class="sxs-lookup"><span data-stu-id="2763e-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="2763e-1424">Obtiene recomendaciones de una compilación concreta de tipo "Recomendación" o "Fbt".</span><span class="sxs-lookup"><span data-stu-id="2763e-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="2763e-1425">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1425">HTTP Method</span></span> | <span data-ttu-id="2763e-1426">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1427">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1428">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1429">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1429">Parameter Name</span></span> | <span data-ttu-id="2763e-1430">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1431">modelId</span></span> |<span data-ttu-id="2763e-1432">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1432">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="2763e-1433">itemIds</span></span> |<span data-ttu-id="2763e-1434">Lista separada por comas de hello elementos toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="2763e-1434">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="2763e-1435">Si compilación activa hello es de tipo FBT, a continuación, puede enviar un único elemento.</span><span class="sxs-lookup"><span data-stu-id="2763e-1435">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="2763e-1436">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="2763e-1436">Max length: 1024</span></span> |
| <span data-ttu-id="2763e-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="2763e-1437">numberOfResults</span></span> |<span data-ttu-id="2763e-1438">Número de resultados obligatorios </span><span class="sxs-lookup"><span data-stu-id="2763e-1438">Number of required results</span></span> <br> <span data-ttu-id="2763e-1439">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="2763e-1439">Max: 150</span></span> |
| <span data-ttu-id="2763e-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="2763e-1440">includeMetatadata</span></span> |<span data-ttu-id="2763e-1441">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="2763e-1441">Future use, always false</span></span> |
| <span data-ttu-id="2763e-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="2763e-1442">buildId</span></span> |<span data-ttu-id="2763e-1443">Hola compilar toouse de identificador para esta solicitud de recomendación</span><span class="sxs-lookup"><span data-stu-id="2763e-1443">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="2763e-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1444">apiVersion</span></span> |<span data-ttu-id="2763e-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1445">1.0</span></span> |

<span data-ttu-id="2763e-1446">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1446">**Response:**</span></span>

<span data-ttu-id="2763e-1447">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1448">respuesta de Hello incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1448">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="2763e-1449">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-1449">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-1450">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="2763e-1451">`Feed\entry\content\properties\Name`-Nombre del elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1451">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="2763e-1452">`Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="2763e-1452">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="2763e-1453">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="2763e-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="2763e-1454">Vea un ejemplo de respuesta en 12.1</span><span class="sxs-lookup"><span data-stu-id="2763e-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="2763e-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="2763e-1455">12.3.</span></span> <span data-ttu-id="2763e-1456">Obtención de recomendaciones de FBT (para la compilación activa)</span><span class="sxs-lookup"><span data-stu-id="2763e-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="2763e-1457">Obtenga recomendaciones de compilación activa de Hola de tipo "Fbt" basada en un elemento de valor de inicialización (entrada).</span><span class="sxs-lookup"><span data-stu-id="2763e-1457">Get recommendations of hello active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="2763e-1458">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1458">HTTP Method</span></span> | <span data-ttu-id="2763e-1459">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1460">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1461">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1462">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1462">Parameter Name</span></span> | <span data-ttu-id="2763e-1463">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1464">modelId</span></span> |<span data-ttu-id="2763e-1465">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1465">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="2763e-1466">itemId</span></span> |<span data-ttu-id="2763e-1467">Elemento toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="2763e-1467">Item toorecommend for.</span></span> <br><span data-ttu-id="2763e-1468">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="2763e-1468">Max length: 1024</span></span> |
| <span data-ttu-id="2763e-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="2763e-1469">numberOfResults</span></span> |<span data-ttu-id="2763e-1470">Número de resultados obligatorios </span><span class="sxs-lookup"><span data-stu-id="2763e-1470">Number of required results</span></span> <br><span data-ttu-id="2763e-1471">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="2763e-1471">Max: 150</span></span> |
| <span data-ttu-id="2763e-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="2763e-1472">minimalScore</span></span> |<span data-ttu-id="2763e-1473">Resultados de puntuación mínima que frecuentes devuelve un conjunto debe haber en toobe orden incluido en hello</span><span class="sxs-lookup"><span data-stu-id="2763e-1473">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="2763e-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="2763e-1474">includeMetatadata</span></span> |<span data-ttu-id="2763e-1475">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="2763e-1475">Future use, always false</span></span> |
| <span data-ttu-id="2763e-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1476">apiVersion</span></span> |<span data-ttu-id="2763e-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1477">1.0</span></span> |

<span data-ttu-id="2763e-1478">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1478">**Response:**</span></span>

<span data-ttu-id="2763e-1479">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1480">respuesta de Hello incluye una entrada por cada conjunto de elementos recomendados (un conjunto de elementos que normalmente se compró junto con el producto de Hola/datos proporcionados por el valor de inicialización).</span><span class="sxs-lookup"><span data-stu-id="2763e-1480">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="2763e-1481">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-1481">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-1482">`Feed\entry\content\properties\Id1`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="2763e-1483">`Feed\entry\content\properties\Name1`-Nombre del elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1483">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="2763e-1484">`Feed\entry\content\properties\Id2`: id. del 2º elemento recomendado (opcional).</span><span class="sxs-lookup"><span data-stu-id="2763e-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="2763e-1485">`Feed\entry\content\properties\Name2`-Nombre del elemento 2 de hello (opcional).</span><span class="sxs-lookup"><span data-stu-id="2763e-1485">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="2763e-1486">`Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="2763e-1486">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="2763e-1487">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="2763e-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="2763e-1488">respuesta de ejemplo de Hola siguiente incluye 3 conjuntos de elementos recomendados.</span><span class="sxs-lookup"><span data-stu-id="2763e-1488">hello example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="2763e-1489">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-1489">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="2763e-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="2763e-1490">12.4.</span></span> <span data-ttu-id="2763e-1491">Obtención de recomendaciones FBT (de una compilación concreta)</span><span class="sxs-lookup"><span data-stu-id="2763e-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="2763e-1492">Obtenga recomendaciones de una compilación concreta de tipo "Fbt".</span><span class="sxs-lookup"><span data-stu-id="2763e-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="2763e-1493">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1493">HTTP Method</span></span> | <span data-ttu-id="2763e-1494">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1495">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1496">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1497">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1497">Parameter Name</span></span> | <span data-ttu-id="2763e-1498">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1499">modelId</span></span> |<span data-ttu-id="2763e-1500">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="2763e-1501">itemId</span></span> |<span data-ttu-id="2763e-1502">Elemento toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="2763e-1502">Item toorecommend for.</span></span> <br><span data-ttu-id="2763e-1503">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="2763e-1503">Max length: 1024</span></span> |
| <span data-ttu-id="2763e-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="2763e-1504">numberOfResults</span></span> |<span data-ttu-id="2763e-1505">Número de resultados obligatorios </span><span class="sxs-lookup"><span data-stu-id="2763e-1505">Number of required results</span></span> <br><span data-ttu-id="2763e-1506">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="2763e-1506">Max: 150</span></span> |
| <span data-ttu-id="2763e-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="2763e-1507">minimalScore</span></span> |<span data-ttu-id="2763e-1508">Resultados de puntuación mínima que frecuentes devuelve un conjunto debe haber en toobe orden incluido en hello</span><span class="sxs-lookup"><span data-stu-id="2763e-1508">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="2763e-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="2763e-1509">includeMetatadata</span></span> |<span data-ttu-id="2763e-1510">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="2763e-1510">Future use, always false</span></span> |
| <span data-ttu-id="2763e-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="2763e-1511">buildId</span></span> |<span data-ttu-id="2763e-1512">Hola compilar toouse de identificador para esta solicitud de recomendación</span><span class="sxs-lookup"><span data-stu-id="2763e-1512">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="2763e-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1513">apiVersion</span></span> |<span data-ttu-id="2763e-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1514">1.0</span></span> |

<span data-ttu-id="2763e-1515">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1515">**Response:**</span></span>

<span data-ttu-id="2763e-1516">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1517">respuesta de Hello incluye una entrada por cada conjunto de elementos recomendados (un conjunto de elementos que normalmente se compró junto con el producto de Hola/datos proporcionados por el valor de inicialización).</span><span class="sxs-lookup"><span data-stu-id="2763e-1517">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="2763e-1518">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-1518">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-1519">`Feed\entry\content\properties\Id1`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="2763e-1520">`Feed\entry\content\properties\Name1`-Nombre del elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1520">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="2763e-1521">`Feed\entry\content\properties\Id2`: id. del 2º elemento recomendado (opcional).</span><span class="sxs-lookup"><span data-stu-id="2763e-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="2763e-1522">`Feed\entry\content\properties\Name2`-Nombre del elemento 2 de hello (opcional).</span><span class="sxs-lookup"><span data-stu-id="2763e-1522">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="2763e-1523">`Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="2763e-1523">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="2763e-1524">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="2763e-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="2763e-1525">Vea un ejemplo de respuesta en 12.3</span><span class="sxs-lookup"><span data-stu-id="2763e-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="2763e-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="2763e-1526">12.5.</span></span> <span data-ttu-id="2763e-1527">Obtención de recomendaciones de usuario (para la compilación activa)</span><span class="sxs-lookup"><span data-stu-id="2763e-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="2763e-1528">Obtenga recomendaciones de la compilación activa de tipo "Recommendation" marcada como compilación activa.</span><span class="sxs-lookup"><span data-stu-id="2763e-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="2763e-1529">Hola API devolverá una lista de elemento de predicción según el historial de uso de toohello del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1529">hello API will return a list of predicted item according toohello usage history of hello user.</span></span>

<span data-ttu-id="2763e-1530">Notas:</span><span class="sxs-lookup"><span data-stu-id="2763e-1530">Notes:</span></span> 

1. <span data-ttu-id="2763e-1531">No hay ninguna recomendación de usuario para la generación de FBT.</span><span class="sxs-lookup"><span data-stu-id="2763e-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="2763e-1532">Si crear Hola active es FBT este método le devuelve un error.</span><span class="sxs-lookup"><span data-stu-id="2763e-1532">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="2763e-1533">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1533">HTTP Method</span></span> | <span data-ttu-id="2763e-1534">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1535">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1536">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1537">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1537">Parameter Name</span></span> | <span data-ttu-id="2763e-1538">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1539">modelId</span></span> |<span data-ttu-id="2763e-1540">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1540">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-1541">userId</span><span class="sxs-lookup"><span data-stu-id="2763e-1541">userId</span></span> |<span data-ttu-id="2763e-1542">Identificador único del usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1542">Unique identifier of hello user</span></span> |
| <span data-ttu-id="2763e-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="2763e-1543">numberOfResults</span></span> |<span data-ttu-id="2763e-1544">Número de resultados requeridos</span><span class="sxs-lookup"><span data-stu-id="2763e-1544">Number of required results</span></span> |
| <span data-ttu-id="2763e-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="2763e-1545">includeMetatadata</span></span> |<span data-ttu-id="2763e-1546">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="2763e-1546">Future use, always false</span></span> |
| <span data-ttu-id="2763e-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1547">apiVersion</span></span> |<span data-ttu-id="2763e-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1548">1.0</span></span> |

<span data-ttu-id="2763e-1549">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1549">**Response:**</span></span>

<span data-ttu-id="2763e-1550">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1551">respuesta de Hello incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1551">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="2763e-1552">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-1552">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-1553">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="2763e-1554">`Feed\entry\content\properties\Name`-Nombre del elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1554">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="2763e-1555">`Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="2763e-1555">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="2763e-1556">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="2763e-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="2763e-1557">Vea un ejemplo de respuesta en 12.1</span><span class="sxs-lookup"><span data-stu-id="2763e-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="2763e-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="2763e-1558">12.6.</span></span> <span data-ttu-id="2763e-1559">Obtención de recomendaciones de usuario con lista de elementos (para la compilación activa)</span><span class="sxs-lookup"><span data-stu-id="2763e-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="2763e-1560">Obtenga recomendaciones de la compilación activa de tipo "Recommendation" marcada como compilación activa con una lista de elementos adicional</span><span class="sxs-lookup"><span data-stu-id="2763e-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="2763e-1561">Hola API devolverá una lista de elemento de predicción según el historial de uso de toohello del usuario de Hola y elementos de hello adicionales proporcionados.</span><span class="sxs-lookup"><span data-stu-id="2763e-1561">hello API will return a list of predicted item according toohello usage history of hello user and hello additional provided items.</span></span>

<span data-ttu-id="2763e-1562">Notas:</span><span class="sxs-lookup"><span data-stu-id="2763e-1562">Notes:</span></span> 

1. <span data-ttu-id="2763e-1563">No hay ninguna recomendación de usuario para la generación de FBT.</span><span class="sxs-lookup"><span data-stu-id="2763e-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="2763e-1564">Si crear Hola active es FBT este método le devuelve un error.</span><span class="sxs-lookup"><span data-stu-id="2763e-1564">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="2763e-1565">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1565">HTTP Method</span></span> | <span data-ttu-id="2763e-1566">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1567">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1568">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1569">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1569">Parameter Name</span></span> | <span data-ttu-id="2763e-1570">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1571">modelId</span></span> |<span data-ttu-id="2763e-1572">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1572">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-1573">userId</span><span class="sxs-lookup"><span data-stu-id="2763e-1573">userId</span></span> |<span data-ttu-id="2763e-1574">Identificador único del usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1574">Unique identifier of hello user</span></span> |
| <span data-ttu-id="2763e-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="2763e-1575">itemsIds</span></span> |<span data-ttu-id="2763e-1576">Lista separada por comas de hello elementos toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="2763e-1576">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="2763e-1577">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="2763e-1577">Max length: 1024</span></span> |
| <span data-ttu-id="2763e-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="2763e-1578">numberOfResults</span></span> |<span data-ttu-id="2763e-1579">Número de resultados requeridos</span><span class="sxs-lookup"><span data-stu-id="2763e-1579">Number of required results</span></span> |
| <span data-ttu-id="2763e-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="2763e-1580">includeMetatadata</span></span> |<span data-ttu-id="2763e-1581">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="2763e-1581">Future use, always false</span></span> |
| <span data-ttu-id="2763e-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1582">apiVersion</span></span> |<span data-ttu-id="2763e-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1583">1.0</span></span> |

<span data-ttu-id="2763e-1584">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1584">**Response:**</span></span>

<span data-ttu-id="2763e-1585">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1586">respuesta de Hello incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1586">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="2763e-1587">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-1587">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-1588">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="2763e-1589">`Feed\entry\content\properties\Name`-Nombre del elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1589">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="2763e-1590">`Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="2763e-1590">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="2763e-1591">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="2763e-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="2763e-1592">Vea un ejemplo de respuesta en 12.1</span><span class="sxs-lookup"><span data-stu-id="2763e-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="2763e-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="2763e-1593">12.7.</span></span> <span data-ttu-id="2763e-1594">Obtención de recomendaciones del usuario (de una compilación concreta)</span><span class="sxs-lookup"><span data-stu-id="2763e-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="2763e-1595">Obtenga recomendaciones de una compilación concreta de tipo "Recomendación" o "Fbt".</span><span class="sxs-lookup"><span data-stu-id="2763e-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="2763e-1596">Hola API devolverá una lista de elemento de predicción según el historial de uso de toohello del usuario de hello (que se usa en la compilación concreta hello).</span><span class="sxs-lookup"><span data-stu-id="2763e-1596">hello API will return a list of predicted item according toohello usage history of hello user (used in hello specific build).</span></span>

<span data-ttu-id="2763e-1597">Nota: no hay ninguna recomendación de usuario para la generación de FBT.</span><span class="sxs-lookup"><span data-stu-id="2763e-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="2763e-1598">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1598">HTTP Method</span></span> | <span data-ttu-id="2763e-1599">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1600">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1601">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1602">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1602">Parameter Name</span></span> | <span data-ttu-id="2763e-1603">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1604">modelId</span></span> |<span data-ttu-id="2763e-1605">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1605">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-1606">userId</span><span class="sxs-lookup"><span data-stu-id="2763e-1606">userId</span></span> |<span data-ttu-id="2763e-1607">Identificador único del usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1607">Unique identifier of hello user</span></span> |
| <span data-ttu-id="2763e-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="2763e-1608">numberOfResults</span></span> |<span data-ttu-id="2763e-1609">Número de resultados requeridos</span><span class="sxs-lookup"><span data-stu-id="2763e-1609">Number of required results</span></span> |
| <span data-ttu-id="2763e-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="2763e-1610">includeMetatadata</span></span> |<span data-ttu-id="2763e-1611">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="2763e-1611">Future use, always false</span></span> |
| <span data-ttu-id="2763e-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="2763e-1612">buildId</span></span> |<span data-ttu-id="2763e-1613">Hola compilar toouse de identificador para esta solicitud de recomendación</span><span class="sxs-lookup"><span data-stu-id="2763e-1613">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="2763e-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1614">apiVersion</span></span> |<span data-ttu-id="2763e-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1615">1.0</span></span> |

<span data-ttu-id="2763e-1616">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1616">**Response:**</span></span>

<span data-ttu-id="2763e-1617">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1618">respuesta de Hello incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1618">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="2763e-1619">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-1619">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-1620">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="2763e-1621">`Feed\entry\content\properties\Name`-Nombre del elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1621">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="2763e-1622">`Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="2763e-1622">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="2763e-1623">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="2763e-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="2763e-1624">Vea un ejemplo de respuesta en 12.1</span><span class="sxs-lookup"><span data-stu-id="2763e-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="2763e-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="2763e-1625">12.8.</span></span> <span data-ttu-id="2763e-1626">Obtención de recomendaciones de usuario con lista de elementos (de una compilación concreta)</span><span class="sxs-lookup"><span data-stu-id="2763e-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="2763e-1627">Obtener recomendaciones de usuario de una compilación concreta del tipo "Recomendación" y lista de Hola de elementos adicionales.</span><span class="sxs-lookup"><span data-stu-id="2763e-1627">Get user recommendations of a specific build of type "Recommendation" and hello list of additional items.</span></span>

<span data-ttu-id="2763e-1628">Hola API devolverá una lista de elemento de predicción según el historial de uso de toohello del usuario de Hola y lista adicional de Hola de elementos.</span><span class="sxs-lookup"><span data-stu-id="2763e-1628">hello API will return a list of predicted item according toohello usage history of hello user and hello additional list of items.</span></span>

<span data-ttu-id="2763e-1629">Nota: no hay ninguna recomendación de usuario para la generación de FBT.</span><span class="sxs-lookup"><span data-stu-id="2763e-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="2763e-1630">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1630">HTTP Method</span></span> | <span data-ttu-id="2763e-1631">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1632">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1633">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1634">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1634">Parameter Name</span></span> | <span data-ttu-id="2763e-1635">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1636">modelId</span></span> |<span data-ttu-id="2763e-1637">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1637">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-1638">userId</span><span class="sxs-lookup"><span data-stu-id="2763e-1638">userId</span></span> |<span data-ttu-id="2763e-1639">Identificador único del usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1639">Unique identifier of hello user</span></span> |
| <span data-ttu-id="2763e-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="2763e-1640">itemIds</span></span> |<span data-ttu-id="2763e-1641">Lista separada por comas de hello elementos toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="2763e-1641">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="2763e-1642">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="2763e-1642">Max length: 1024</span></span> |
| <span data-ttu-id="2763e-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="2763e-1643">numberOfResults</span></span> |<span data-ttu-id="2763e-1644">Número de resultados requeridos</span><span class="sxs-lookup"><span data-stu-id="2763e-1644">Number of required results</span></span> |
| <span data-ttu-id="2763e-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="2763e-1645">includeMetatadata</span></span> |<span data-ttu-id="2763e-1646">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="2763e-1646">Future use, always false</span></span> |
| <span data-ttu-id="2763e-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="2763e-1647">buildId</span></span> |<span data-ttu-id="2763e-1648">Hola compilar toouse de identificador para esta solicitud de recomendación</span><span class="sxs-lookup"><span data-stu-id="2763e-1648">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="2763e-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1649">apiVersion</span></span> |<span data-ttu-id="2763e-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1650">1.0</span></span> |

<span data-ttu-id="2763e-1651">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1651">**Response:**</span></span>

<span data-ttu-id="2763e-1652">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1653">respuesta de Hello incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1653">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="2763e-1654">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-1654">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-1655">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="2763e-1656">`Feed\entry\content\properties\Name`-Nombre del elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1656">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="2763e-1657">`Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="2763e-1657">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="2763e-1658">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="2763e-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="2763e-1659">Vea un ejemplo de respuesta en 12.1</span><span class="sxs-lookup"><span data-stu-id="2763e-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="2763e-1660">13. Historial de uso del usuario</span><span class="sxs-lookup"><span data-stu-id="2763e-1660">13. User Usage History</span></span>
<span data-ttu-id="2763e-1661">Una vez que se creó un modelo de recomendación sistema Hola permitirá tooretrieve historial de usuarios de hello (usuario específico de elementos asociados tooa) utilizado para la compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1661">Once a recommendation model was built hello system will allow tooretrieve hello user history (items associated tooa specific user) used for hello build.</span></span>
<span data-ttu-id="2763e-1662">Esta API permitir que el historial de usuario de hello tooretrieve</span><span class="sxs-lookup"><span data-stu-id="2763e-1662">This API allow tooretrieve hello user history</span></span>

<span data-ttu-id="2763e-1663">Nota: historial de usuarios de hello actualmente solo está disponible para compilaciones de recomendación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1663">Note: hello user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="2763e-1664">13.1 Recuperación del historial del usuario</span><span class="sxs-lookup"><span data-stu-id="2763e-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="2763e-1665">Recupera la lista de Hola de elemento utilizado en hello active generar u Hola especifica compilar para hello tiene el Id. de usuario.</span><span class="sxs-lookup"><span data-stu-id="2763e-1665">Retrieve hello list of item used in hello active build or in hello specified build for hello given user id.</span></span>

| <span data-ttu-id="2763e-1666">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1666">HTTP Method</span></span> | <span data-ttu-id="2763e-1667">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1668">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1668">GET</span></span> |<span data-ttu-id="2763e-1669">Obtener el historial de usuario de Hola de compilación activa Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1669">Get hello user history for hello active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="2763e-1670">Obtener historial de usuarios de Hola Hola proporcionado compilación`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="2763e-1670">Get hello user history for hello given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="2763e-1671">Ejemplo:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="2763e-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="2763e-1672">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1672">Parameter Name</span></span> | <span data-ttu-id="2763e-1673">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1674">modelId</span></span> |<span data-ttu-id="2763e-1675">Identificador único de Hello del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1675">hello unique identifier of hello model.</span></span> |
| <span data-ttu-id="2763e-1676">userId</span><span class="sxs-lookup"><span data-stu-id="2763e-1676">userId</span></span> |<span data-ttu-id="2763e-1677">Hola identificador único del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1677">hello unique identifier of hello user.</span></span> |
| <span data-ttu-id="2763e-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="2763e-1678">buildId</span></span> |<span data-ttu-id="2763e-1679">parámetro opcional, permitir tooindicate desde la compilación de historial de usuarios de hello debe ser fetch</span><span class="sxs-lookup"><span data-stu-id="2763e-1679">optional parameter, allow tooindicate from which build hello user history should be fetch</span></span> |
| <span data-ttu-id="2763e-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1680">apiVersion</span></span> |<span data-ttu-id="2763e-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1681">1.0</span></span> |

<span data-ttu-id="2763e-1682">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1682">**Response:**</span></span>

<span data-ttu-id="2763e-1683">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1684">respuesta de Hello incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1684">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="2763e-1685">Cada entrada tiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2763e-1685">Each entry has hello following data:</span></span>

* <span data-ttu-id="2763e-1686">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="2763e-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="2763e-1687">`Feed\entry\content\properties\Name`-Nombre del elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1687">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="2763e-1688">`Feed\entry\content\properties\Rating` : N/D.</span><span class="sxs-lookup"><span data-stu-id="2763e-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="2763e-1689">`Feed\entry\content\properties\Reasoning` : N/D.</span><span class="sxs-lookup"><span data-stu-id="2763e-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="2763e-1690">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-1690">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a><span data-ttu-id="2763e-1691">14. Notificaciones</span><span class="sxs-lookup"><span data-stu-id="2763e-1691">14. Notifications</span></span>
<span data-ttu-id="2763e-1692">Recomendaciones de aprendizaje de máquina Azure crea notificaciones cuando se producen los errores persistentes en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in hello system.</span></span> <span data-ttu-id="2763e-1693">Hay 3 tipos de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="2763e-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="2763e-1694">Error de compilación: esta notificación se desencadena con cada error de compilación.</span><span class="sxs-lookup"><span data-stu-id="2763e-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="2763e-1695">Error - esta notificación de procesamiento de adquisición de datos se desencadena cuando se tienen más de 100 errores en hello últimos 5 minutos en el procesamiento de Hola de eventos de uso por el modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of usage events per model.</span></span>
3. <span data-ttu-id="2763e-1696">Error de consumo de recomendación: esta notificación se desencadena cuando se tienen más de 100 errores en hello últimos 5 minutos en el procesamiento de Hola de solicitudes de recomendación por modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="2763e-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="2763e-1697">14.1.</span></span> <span data-ttu-id="2763e-1698">Obtener notificaciones</span><span class="sxs-lookup"><span data-stu-id="2763e-1698">Get Notifications</span></span>
<span data-ttu-id="2763e-1699">Recupera todas las notificaciones de Hola para todos los modelos o para un único modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1699">Retrieves all hello notifications for all models or for a single model.</span></span>

| <span data-ttu-id="2763e-1700">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1700">HTTP Method</span></span> | <span data-ttu-id="2763e-1701">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1702">GET</span><span class="sxs-lookup"><span data-stu-id="2763e-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1703">Obtener todas las notificaciones de todos los modelos:</span><span class="sxs-lookup"><span data-stu-id="2763e-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1704">Ejemplo de obtener las notificaciones para un modelo específico:</span><span class="sxs-lookup"><span data-stu-id="2763e-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="2763e-1705">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1705">Parameter Name</span></span> | <span data-ttu-id="2763e-1706">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1707">modelId</span></span> |<span data-ttu-id="2763e-1708">Parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="2763e-1708">Optional parameter.</span></span> <span data-ttu-id="2763e-1709">Cuando se omite, obtendrá todas las notificaciones para todos los modelos.</span><span class="sxs-lookup"><span data-stu-id="2763e-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="2763e-1710">Valor válido: identificador único del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2763e-1710">Valid value: unique identifier of hello model.</span></span> |
| <span data-ttu-id="2763e-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1711">apiVersion</span></span> |<span data-ttu-id="2763e-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-1713">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-1713">Request Body</span></span> |<span data-ttu-id="2763e-1714">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-1714">NONE</span></span> |

<span data-ttu-id="2763e-1715">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="2763e-1715">**Response:**</span></span>

<span data-ttu-id="2763e-1716">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="2763e-1717">OData XML</span><span class="sxs-lookup"><span data-stu-id="2763e-1717">OData XML</span></span>

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a><span data-ttu-id="2763e-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="2763e-1718">14.2.</span></span> <span data-ttu-id="2763e-1719">Eliminar notificaciones de modelo</span><span class="sxs-lookup"><span data-stu-id="2763e-1719">Delete Model Notifications</span></span>
<span data-ttu-id="2763e-1720">Elimina todas las notificaciones de lectura para un modelo.</span><span class="sxs-lookup"><span data-stu-id="2763e-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="2763e-1721">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1721">HTTP Method</span></span> | <span data-ttu-id="2763e-1722">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1723">DELETE</span><span class="sxs-lookup"><span data-stu-id="2763e-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2763e-1724">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2763e-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1725">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1725">Parameter Name</span></span> | <span data-ttu-id="2763e-1726">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="2763e-1727">modelId</span></span> |<span data-ttu-id="2763e-1728">Identificador único del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="2763e-1728">Unique identifier of hello model</span></span> |
| <span data-ttu-id="2763e-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1729">apiVersion</span></span> |<span data-ttu-id="2763e-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-1731">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-1731">Request Body</span></span> |<span data-ttu-id="2763e-1732">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-1732">NONE</span></span> |

<span data-ttu-id="2763e-1733">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-1733">**Response**:</span></span>

<span data-ttu-id="2763e-1734">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="2763e-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="2763e-1735">14.3.</span></span> <span data-ttu-id="2763e-1736">Eliminar notificaciones de usuario</span><span class="sxs-lookup"><span data-stu-id="2763e-1736">Delete User Notifications</span></span>
<span data-ttu-id="2763e-1737">Elimina todas las notificaciones para todos los modelos.</span><span class="sxs-lookup"><span data-stu-id="2763e-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="2763e-1738">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="2763e-1738">HTTP Method</span></span> | <span data-ttu-id="2763e-1739">URI</span><span class="sxs-lookup"><span data-stu-id="2763e-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1740">DELETE</span><span class="sxs-lookup"><span data-stu-id="2763e-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="2763e-1741">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="2763e-1741">Parameter Name</span></span> | <span data-ttu-id="2763e-1742">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="2763e-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2763e-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2763e-1743">apiVersion</span></span> |<span data-ttu-id="2763e-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="2763e-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="2763e-1745">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="2763e-1745">Request Body</span></span> |<span data-ttu-id="2763e-1746">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="2763e-1746">NONE</span></span> |

<span data-ttu-id="2763e-1747">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="2763e-1747">**Response**:</span></span>

<span data-ttu-id="2763e-1748">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2763e-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="2763e-1749">15. Información legal</span><span class="sxs-lookup"><span data-stu-id="2763e-1749">15. Legal</span></span>
<span data-ttu-id="2763e-1750">Este documento se proporciona "como está".</span><span class="sxs-lookup"><span data-stu-id="2763e-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="2763e-1751">La información y las opiniones expresadas en este documento, como las direcciones URL y otras referencias a sitios web de Internet, pueden cambiar sin previo aviso.</span><span class="sxs-lookup"><span data-stu-id="2763e-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="2763e-1752">Algunos ejemplos mencionados se proporcionan únicamente con fines ilustrativos y son ficticios.</span><span class="sxs-lookup"><span data-stu-id="2763e-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="2763e-1753">No se pretende ninguna asociación o conexión real ni debe deducirse.</span><span class="sxs-lookup"><span data-stu-id="2763e-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="2763e-1754">Este documento no proporcionan ningún derecho legal tooany la propiedad intelectual de ningún producto de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2763e-1754">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="2763e-1755">Puede copiar y usar este documento con fines internos y de referencia.</span><span class="sxs-lookup"><span data-stu-id="2763e-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="2763e-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2763e-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="2763e-1757">Todos los derechos reservados.</span><span class="sxs-lookup"><span data-stu-id="2763e-1757">All rights reserved.</span></span>

