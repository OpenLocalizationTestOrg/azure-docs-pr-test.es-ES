---
title: "Documentación de la API de recomendaciones de Machine Learning | Microsoft Docs"
description: "Documentación de la API de recomendaciones de Aprendizaje automático de Azure para un motor de recomendaciones disponible en Microsoft Azure Marketplace."
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
redirect_document_id: TRUE
ms.openlocfilehash: 1fba64d78d779344e2895b0d54419186b7584865
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="64f48-103">Documentación de la API de recomendación de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="64f48-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="64f48-104">Debe empezar a utilizar el servicio Cognitive Services de la API de Recomendaciones en lugar de esta versión.</span><span class="sxs-lookup"><span data-stu-id="64f48-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="64f48-105">El servicio Cognitive Services de Recomendaciones va a sustituir a este servicio y todas las características nuevas se desarrollarán en esta nueva versión.</span><span class="sxs-lookup"><span data-stu-id="64f48-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="64f48-106">Tiene nuevas funcionalidades como compatibilidad con procesamientos por lotes, un explorador de API más eficaz, una interfaz de API más limpia, una experiencia de facturación y suscripción más coherente, etc.</span><span class="sxs-lookup"><span data-stu-id="64f48-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="64f48-107">Obtenga más información sobre cómo [migrar al nuevo servicio Cognitive Services](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="64f48-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="64f48-108">Este documento describe las API de recomendaciones de Aprendizaje automático de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="64f48-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="64f48-109">1. Información general</span><span class="sxs-lookup"><span data-stu-id="64f48-109">1. General overview</span></span>
<span data-ttu-id="64f48-110">Este documento es una referencia de API.</span><span class="sxs-lookup"><span data-stu-id="64f48-110">This document is an API reference.</span></span> <span data-ttu-id="64f48-111">Debe empezar con el documento "Recomendación de Aprendizaje automático de Azure: Inicio rápido".</span><span class="sxs-lookup"><span data-stu-id="64f48-111">You should start with the “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="64f48-112">La API de recomendaciones de Aprendizaje automático de Azure se puede dividir en los grupos lógicos siguientes:</span><span class="sxs-lookup"><span data-stu-id="64f48-112">The Azure Machine Learning Recommendations API can be divided into the following logical groups:</span></span>

* <span data-ttu-id="64f48-113"><ins>Limitaciones</ins>: Limitaciones de la API de recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="64f48-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="64f48-114"><ins>Información general</ins>: Información sobre la autenticación, el identificador URI de servicio y el control de versiones.</span><span class="sxs-lookup"><span data-stu-id="64f48-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="64f48-115"><ins>Modelo básico</ins>: las API que le permiten realizar las operaciones básicas en el modelo (por ejemplo, crear, actualizar y eliminar un modelo).</span><span class="sxs-lookup"><span data-stu-id="64f48-115"><ins>Model Basic</ins> - APIs that enable you to do the basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="64f48-116"><ins>Modelo avanzado</ins>: las API que le permiten obtener información avanzada de datos en el modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-116"><ins>Model Advanced</ins> - APIs that enable you to get advanced data insights on the model.</span></span>
* <span data-ttu-id="64f48-117"><ins>Reglas de negocio de modelo</ins>: las API que le permiten administrar reglas de negocio en los resultados de recomendación de modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-117"><ins>Model Business Rules</ins> - APIs that enable you to manage business rules on the model recommendation results.</span></span>
* <span data-ttu-id="64f48-118"><ins>Catálogo</ins>: las API que le permiten realizar operaciones básicas en un catálogo de modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-118"><ins>Catalog</ins> - APIs that enable you to do basic operations on a model catalog.</span></span> <span data-ttu-id="64f48-119">Un catálogo contiene información de metadatos sobre los elementos de los datos de uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-119">A catalog contains metadata information on the items of the usage data.</span></span>
* <span data-ttu-id="64f48-120"><ins>Característica</ins>: Las API que permiten obtener información sobre el elemento del catálogo y cómo usar esta información para crear mejores recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="64f48-120"><ins>Feature</ins> - APIs that enable to get insights on item into the catalog and how to use this information to build better recommendations.</span></span>
* <span data-ttu-id="64f48-121"><ins>Datos de uso</ins>: las API que le permiten realizar operaciones básicas en los datos de uso del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-121"><ins>Usage Data</ins> - APIs that enable you to do basic operations on the model usage data.</span></span> <span data-ttu-id="64f48-122">Los datos de uso de la forma básica constan de filas que incluyen pares de &#60;userId&#62;,&#60;itemId&#62;.</span><span class="sxs-lookup"><span data-stu-id="64f48-122">Usage data in the basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="64f48-123"><ins>Compilación</ins>: las API que le permiten desencadenar una compilación de modelo y realizar operaciones básicas relacionadas con esta compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-123"><ins>Build</ins> - APIs that enable you to trigger a model build and do basic operations that are related to this build.</span></span> <span data-ttu-id="64f48-124">Puede desencadenar una compilación de modelo una vez que tenga datos de uso valiosos.</span><span class="sxs-lookup"><span data-stu-id="64f48-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="64f48-125"><ins>Recomendación</ins>: las API que le permiten usar recomendaciones una vez que la compilación de un modelo finaliza.</span><span class="sxs-lookup"><span data-stu-id="64f48-125"><ins>Recommendation</ins> - APIs that enable you to consume recommendations once the build of a model ends.</span></span>
* <span data-ttu-id="64f48-126"><ins>Datos de usuario</ins>las API que le permiten capturar información sobre los datos de uso del usuario.</span><span class="sxs-lookup"><span data-stu-id="64f48-126"><ins>User Data</ins> - APIs that enable you to fetch information on the user usage data.</span></span>
* <span data-ttu-id="64f48-127"><ins>Notificaciones</ins>: las API que le permiten recibir notificaciones acerca de los problemas relacionados con las operaciones de API.</span><span class="sxs-lookup"><span data-stu-id="64f48-127"><ins>Notifications</ins> - APIs that enable you to receive notifications on problems related to your API operations.</span></span> <span data-ttu-id="64f48-128">(Por ejemplo, notifica el uso de los datos a través de la adquisición de datos y la mayor parte del procesamiento de eventos está dando errores.</span><span class="sxs-lookup"><span data-stu-id="64f48-128">(For example, you are reporting usage data via Data Acquisition and most of the events processing are failing.</span></span> <span data-ttu-id="64f48-129">Se generará una notificación de error).</span><span class="sxs-lookup"><span data-stu-id="64f48-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="64f48-130">2. Limitaciones</span><span class="sxs-lookup"><span data-stu-id="64f48-130">2. Limitations</span></span>
* <span data-ttu-id="64f48-131">El número máximo de modelos por suscripción es 10.</span><span class="sxs-lookup"><span data-stu-id="64f48-131">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="64f48-132">El número máximo de compilaciones por modelo es 20.</span><span class="sxs-lookup"><span data-stu-id="64f48-132">The maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="64f48-133">El número máximo de elementos que puede contener un catálogo es 100 000.</span><span class="sxs-lookup"><span data-stu-id="64f48-133">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="64f48-134">El número máximo de puntos de uso que se mantienen es ~ 5 000 000.</span><span class="sxs-lookup"><span data-stu-id="64f48-134">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="64f48-135">Se eliminarán los más antiguos si se cargan o notifican unos nuevos.</span><span class="sxs-lookup"><span data-stu-id="64f48-135">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="64f48-136">El tamaño máximo de datos que puede enviarse en POST (por ejemplo, importar datos de catálogo, importar datos de uso) es de 200 MB</span><span class="sxs-lookup"><span data-stu-id="64f48-136">The maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="64f48-137">El número máximo de elementos que se pueden solicitar al obtener recomendaciones es 150.</span><span class="sxs-lookup"><span data-stu-id="64f48-137">The maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="64f48-138">3. API: información general</span><span class="sxs-lookup"><span data-stu-id="64f48-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="64f48-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="64f48-139">3.1.</span></span> <span data-ttu-id="64f48-140">Autenticación</span><span class="sxs-lookup"><span data-stu-id="64f48-140">Authentication</span></span>
<span data-ttu-id="64f48-141">Siga las directrices de Microsoft Azure Marketplace con respecto a la autenticación.</span><span class="sxs-lookup"><span data-stu-id="64f48-141">Please follow the Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="64f48-142">Marketplace admite métodos de autenticación Básica o OAuth.</span><span class="sxs-lookup"><span data-stu-id="64f48-142">The marketplace supports either the Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="64f48-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-143">3.2.</span></span> <span data-ttu-id="64f48-144">URI de servicio</span><span class="sxs-lookup"><span data-stu-id="64f48-144">Service URI</span></span>
<span data-ttu-id="64f48-145">El URI raíz de servicio para cada una de las API de recomendaciones de Aprendizaje automático de Azure se encuentra [aquí](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="64f48-145">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="64f48-146">El URI de servicio completo se expresa mediante elementos de la especificación de OData.</span><span class="sxs-lookup"><span data-stu-id="64f48-146">The full service URI is expressed using elements of the OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="64f48-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="64f48-147">3.3.</span></span> <span data-ttu-id="64f48-148">Versión de API</span><span class="sxs-lookup"><span data-stu-id="64f48-148">API version</span></span>
<span data-ttu-id="64f48-149">Cada llamada a la API tendrá al final el parámetro de consulta denominado apiVersion que debe estar establecido en 1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-149">Each API call will have, at the end, a query parameter called apiVersion that should be set to 1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="64f48-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="64f48-150">3.4.</span></span> <span data-ttu-id="64f48-151">Los Id. distinguen mayúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="64f48-151">IDs are case sensitive</span></span>
<span data-ttu-id="64f48-152">Los Id., devueltos por cualquiera de las API, distinguen mayúsculas de minúsculas y deben usarse como tales cuando se pasan como parámetros en las sucesivas llamadas a API.</span><span class="sxs-lookup"><span data-stu-id="64f48-152">IDs, returned by any of the APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="64f48-153">Por ejemplo, los Id. de modelo y de catálogo distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="64f48-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="64f48-154">4. Calidad de recomendaciones y elementos fríos</span><span class="sxs-lookup"><span data-stu-id="64f48-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="64f48-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="64f48-155">4.1.</span></span> <span data-ttu-id="64f48-156">Calidad de recomendación</span><span class="sxs-lookup"><span data-stu-id="64f48-156">Recommendation quality</span></span>
<span data-ttu-id="64f48-157">La creación de un modelo de recomendación suele ser suficiente para permitir que el sistema proporcione recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="64f48-157">Creating a recommendation model is usually enough to allow the system to provide recommendations.</span></span> <span data-ttu-id="64f48-158">No obstante, la calidad de recomendación varía según el uso procesado y la cobertura del catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-158">Nevertheless, recommendation quality varies based on the usage processed and the coverage of the catalog.</span></span> <span data-ttu-id="64f48-159">Por ejemplo si tiene muchos elementos fríos (sin uso significativo), el sistema tendrá dificultades para proporcionar una recomendación para un elemento de este tipo o para usar un elemento de este tipo como recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-159">For example if you have a lot of cold items (items without significant usage), the system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="64f48-160">Para solucionar el problema con los elementos fríos, el sistema permite el uso de metadatos de los elementos para mejorar las recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="64f48-160">In order to overcome the cold item problem, the system allows the use of metadata of the items to enhance the recommendations.</span></span> <span data-ttu-id="64f48-161">Estos metadatos se conocen como características.</span><span class="sxs-lookup"><span data-stu-id="64f48-161">This metadata is referred to as features.</span></span> <span data-ttu-id="64f48-162">Características típicas son el autor de un libro o el actor de una película.</span><span class="sxs-lookup"><span data-stu-id="64f48-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="64f48-163">Las características se proporcionan mediante el catálogo en forma de cadenas de clave y valor.</span><span class="sxs-lookup"><span data-stu-id="64f48-163">Features are provided via the catalog in the form of key/value strings.</span></span> <span data-ttu-id="64f48-164">Para obtener el formato completo del archivo de catálogo, consulte la [sección sobre la importación del catálogo](#81-import-catalog-data).</span><span class="sxs-lookup"><span data-stu-id="64f48-164">For the full format of the catalog file, please refer to the [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="64f48-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-165">4.2.</span></span> <span data-ttu-id="64f48-166">Compilación de rango</span><span class="sxs-lookup"><span data-stu-id="64f48-166">Rank build</span></span>
<span data-ttu-id="64f48-167">Las características pueden mejorar el modelo de recomendación, pero para ello se requiere el uso de características significativas.</span><span class="sxs-lookup"><span data-stu-id="64f48-167">Features can enhance the recommendation model, but to do so requires the use of meaningful features.</span></span> <span data-ttu-id="64f48-168">Con este fin se introdujo una nueva compilación, una compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="64f48-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="64f48-169">Esta compilación clasifica la utilidad de las características.</span><span class="sxs-lookup"><span data-stu-id="64f48-169">This build will rank the usefulness of features.</span></span> <span data-ttu-id="64f48-170">Una característica significativa es una característica con una puntuación de rango de 2 para arriba.</span><span class="sxs-lookup"><span data-stu-id="64f48-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="64f48-171">Una vez que conozca cuáles de las características son significativas, desencadene una compilación de recomendación con la lista (o sublista) de características significativas.</span><span class="sxs-lookup"><span data-stu-id="64f48-171">After understanding which of the features are meaningful, trigger a recommendation build with the list (or sublist) of meaningful features.</span></span> <span data-ttu-id="64f48-172">Es posible utilizar estas características para la mejora de los elementos fríos y calientes.</span><span class="sxs-lookup"><span data-stu-id="64f48-172">It is possible to use these feature for the enhancement of both warm items and cold items.</span></span> <span data-ttu-id="64f48-173">Para poder usarlas con los elementos calientes, se debe configurar el parámetro de compilación `UseFeatureInModel` .</span><span class="sxs-lookup"><span data-stu-id="64f48-173">In order to use them for warm items, the `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="64f48-174">Para poder usarlas con los elementos fríos, se debe configurar el parámetro de compilación `AllowColdItemPlacement` .</span><span class="sxs-lookup"><span data-stu-id="64f48-174">In order to use features for cold items, the `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="64f48-175">Nota: no es posible habilitar `AllowColdItemPlacement` sin habilitar `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="64f48-175">Note: It is not possible to enable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="64f48-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="64f48-176">4.3.</span></span> <span data-ttu-id="64f48-177">Razonamiento de recomendación</span><span class="sxs-lookup"><span data-stu-id="64f48-177">Recommendation reasoning</span></span>
<span data-ttu-id="64f48-178">El razonamiento de la recomendación es otro aspecto del uso de características.</span><span class="sxs-lookup"><span data-stu-id="64f48-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="64f48-179">De hecho, el motor de recomendaciones de Azure Machine Learning puede utilizar funciones para proporcionar explicaciones de recomendación (también conocidas como</span><span class="sxs-lookup"><span data-stu-id="64f48-179">Indeed, the Azure Machine Learning Recommendations engine can use features to provide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="64f48-180">razonamientos), lo que conduce a una mayor confianza en el elemento recomendado del consumidor de la recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-180">reasoning), leading to more confidence in the recommended item from the recommendation consumer.</span></span>
<span data-ttu-id="64f48-181">Para habilitar el razonamiento, los parámetros `AllowFeatureCorrelation` y `ReasoningFeatureList` deben configurarse antes de solicitar una compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-181">To enable reasoning, the `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior to requesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="64f48-182">5. Modelo básico</span><span class="sxs-lookup"><span data-stu-id="64f48-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="64f48-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="64f48-183">5.1.</span></span> <span data-ttu-id="64f48-184">Crear modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-184">Create Model</span></span>
<span data-ttu-id="64f48-185">Crea una solicitud "crear modelo".</span><span class="sxs-lookup"><span data-stu-id="64f48-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="64f48-186">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-186">HTTP Method</span></span> | <span data-ttu-id="64f48-187">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-188">POST</span><span class="sxs-lookup"><span data-stu-id="64f48-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-189">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-190">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-190">Parameter Name</span></span> | <span data-ttu-id="64f48-191">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-192">modelName</span><span class="sxs-lookup"><span data-stu-id="64f48-192">modelName</span></span> |<span data-ttu-id="64f48-193">Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="64f48-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="64f48-194">Longitud máxima: 20</span><span class="sxs-lookup"><span data-stu-id="64f48-194">Max length: 20</span></span> |
| <span data-ttu-id="64f48-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-195">apiVersion</span></span> |<span data-ttu-id="64f48-196">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-196">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-197">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-197">Request Body</span></span> |<span data-ttu-id="64f48-198">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-198">NONE</span></span> |

<span data-ttu-id="64f48-199">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-199">**Response**:</span></span>

<span data-ttu-id="64f48-200">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="64f48-201">`feed/entry/content/properties/id`: contiene el id. de modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-201">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="64f48-202">**Nota**: el Id. de modelo distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="64f48-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="64f48-203">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-203">OData XML</span></span>

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

### <a name="52-get-model"></a><span data-ttu-id="64f48-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-204">5.2.</span></span> <span data-ttu-id="64f48-205">Obtener modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-205">Get Model</span></span>
<span data-ttu-id="64f48-206">Crea una solicitud "obtener modelo".</span><span class="sxs-lookup"><span data-stu-id="64f48-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="64f48-207">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-207">HTTP Method</span></span> | <span data-ttu-id="64f48-208">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-209">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="64f48-210">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-211">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-211">Parameter Name</span></span> | <span data-ttu-id="64f48-212">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-213">id</span><span class="sxs-lookup"><span data-stu-id="64f48-213">id</span></span> |<span data-ttu-id="64f48-214">El identificador único del modelo  (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="64f48-214">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="64f48-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-215">apiVersion</span></span> |<span data-ttu-id="64f48-216">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-216">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-217">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-217">Request Body</span></span> |<span data-ttu-id="64f48-218">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-218">NONE</span></span> |

<span data-ttu-id="64f48-219">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-219">**Response**:</span></span>

<span data-ttu-id="64f48-220">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-220">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-221">Los datos del modelo pueden encontrarse en los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="64f48-221">The model data can be found under the following elements:</span></span>

* <span data-ttu-id="64f48-222">`feed/entry/content/properties/Id`: id. único de modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="64f48-223">`feed/entry/content/properties/Name`: nombre del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="64f48-224">`feed/entry/content/properties/Date` : fecha de creación del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="64f48-225">`feed/entry/content/properties/Status` : estado del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="64f48-226">Uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="64f48-226">One of the following:</span></span>
  * <span data-ttu-id="64f48-227">Created: el modelo se crea y no contiene Catálogo ni Uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="64f48-228">ReadyForBuild: el modelo se crea y contiene Catálogo y Uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="64f48-229">`feed/entry/content/properties/HasActiveBuild`: indica si el modelo se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="64f48-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span></span>
* <span data-ttu-id="64f48-230">`feed/entry/content/properties/BuildId` : id. de compilación activa del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="64f48-231">`feed/entry/content/properties/Mpr`: clasificación percentil de promedio del modelo (MPR, consulte ModelInsight para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="64f48-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="64f48-232">`feed/entry/content/properties/UserName` : nombre de usuario interno del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="64f48-233">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-233">OData XML</span></span>

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

### <a name="53----get-all-models"></a><span data-ttu-id="64f48-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="64f48-234">5.3.</span></span>    <span data-ttu-id="64f48-235">Obtener todos los modelos</span><span class="sxs-lookup"><span data-stu-id="64f48-235">Get All Models</span></span>
<span data-ttu-id="64f48-236">Recupera todos los modelos del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="64f48-236">Retrieves all models of the current user.</span></span>

| <span data-ttu-id="64f48-237">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-237">HTTP Method</span></span> | <span data-ttu-id="64f48-238">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-239">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="64f48-240">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-241">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-241">Parameter Name</span></span> | <span data-ttu-id="64f48-242">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-243">apiVersion</span></span> |<span data-ttu-id="64f48-244">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-244">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-245">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-245">Request Body</span></span> |<span data-ttu-id="64f48-246">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-246">NONE</span></span> |

<span data-ttu-id="64f48-247">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-247">**Response**:</span></span>

<span data-ttu-id="64f48-248">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="64f48-249">`feed/entry/content/properties/Id`: id. único de modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="64f48-250">`feed/entry/content/properties/Name`: nombre del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="64f48-251">`feed/entry/content/properties/Date` : fecha de creación del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="64f48-252">`feed/entry/content/properties/Status` : estado del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="64f48-253">Uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="64f48-253">One of the following:</span></span>
  * <span data-ttu-id="64f48-254">Created: el modelo se crea y no contiene Catálogo ni Uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="64f48-255">ReadyForBuild: el modelo se crea y contiene Catálogo y Uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="64f48-256">`feed/entry/content/properties/HasActiveBuild`: indica si el modelo se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="64f48-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span></span>
* <span data-ttu-id="64f48-257">`feed/entry/content/properties/BuildId` : id. de compilación activa del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="64f48-258">`feed/entry/content/properties/Mpr`: MPR del modelo (consulte ModelInsight para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="64f48-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="64f48-259">`feed/entry/content/properties/UserName` : nombre de usuario interno del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="64f48-260">`feed/entry/content/properties/UsageFileNames`: lista de archivos de uso del modelo separados por coma.</span><span class="sxs-lookup"><span data-stu-id="64f48-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="64f48-261">`feed/entry/content/properties/CatalogId`: id. de catálogo del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="64f48-262">`feed/entry/content/properties/Description`: descripción del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="64f48-263">`feed/entry/content/properties/CatalogFileName` : nombre de archivo del catálogo de modelos.</span><span class="sxs-lookup"><span data-stu-id="64f48-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="64f48-264">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-264">OData XML</span></span>

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

### <a name="54----update-model"></a><span data-ttu-id="64f48-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="64f48-265">5.4.</span></span>    <span data-ttu-id="64f48-266">Actualizar modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-266">Update Model</span></span>
<span data-ttu-id="64f48-267">Puede actualizar la descripción del modelo o el identificador de compilación activa.</span><span class="sxs-lookup"><span data-stu-id="64f48-267">You can update the model description or the active build ID.</span></span><br><span data-ttu-id="64f48-268">
<ins>Id. de compilación activa</ins>: cada compilación para cada modelo tiene un identificador de compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="64f48-269">El Id. de compilación activa es la primera compilación correcta de cada nuevo modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-269">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="64f48-270">Una vez que tiene un Id. de compilación activa y realiza compilaciones adicionales para el mismo modelo, necesitará establecerlo explícitamente como el Id. de compilación predeterminado si lo desea.</span><span class="sxs-lookup"><span data-stu-id="64f48-270">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="64f48-271">Cuando se usan las recomendaciones, si no especifica el identificador de compilación que desea usar, se utilizará automáticamente el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="64f48-271">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span><br>
<span data-ttu-id="64f48-272">Este mecanismo le permite tener un modelo de recomendación en producción para compilar nuevos modelos y probarlos antes de promoverlos a producción.</span><span class="sxs-lookup"><span data-stu-id="64f48-272">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="64f48-273">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-273">HTTP Method</span></span> | <span data-ttu-id="64f48-274">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-275">PUT</span><span class="sxs-lookup"><span data-stu-id="64f48-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="64f48-276">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-277">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-277">Parameter Name</span></span> | <span data-ttu-id="64f48-278">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-279">id</span><span class="sxs-lookup"><span data-stu-id="64f48-279">id</span></span> |<span data-ttu-id="64f48-280">El identificador único del modelo  (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="64f48-280">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="64f48-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-281">apiVersion</span></span> |<span data-ttu-id="64f48-282">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-282">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-283">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="64f48-284">Tenga en cuenta que las etiquetas XML Description y ActiveBuildId son opcionales.</span><span class="sxs-lookup"><span data-stu-id="64f48-284">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="64f48-285">Si no desea establecer Description o ActiveBuildId, elimine la etiqueta entera.</span><span class="sxs-lookup"><span data-stu-id="64f48-285">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="64f48-286">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-286">**Response**:</span></span>

<span data-ttu-id="64f48-287">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="64f48-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="64f48-288">5.5.</span></span>    <span data-ttu-id="64f48-289">Eliminar modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-289">Delete Model</span></span>
<span data-ttu-id="64f48-290">Elimina un modelo existente por el Id.</span><span class="sxs-lookup"><span data-stu-id="64f48-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="64f48-291">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-291">HTTP Method</span></span> | <span data-ttu-id="64f48-292">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-293">DELETE</span><span class="sxs-lookup"><span data-stu-id="64f48-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="64f48-294">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-295">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-295">Parameter Name</span></span> | <span data-ttu-id="64f48-296">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-297">id</span><span class="sxs-lookup"><span data-stu-id="64f48-297">id</span></span> |<span data-ttu-id="64f48-298">El identificador único del modelo  (distingue mayúsculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="64f48-298">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="64f48-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-299">apiVersion</span></span> |<span data-ttu-id="64f48-300">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-300">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-301">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-301">Request Body</span></span> |<span data-ttu-id="64f48-302">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-302">NONE</span></span> |

<span data-ttu-id="64f48-303">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-303">**Response**:</span></span>

<span data-ttu-id="64f48-304">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-304">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-305">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-305">OData XML</span></span>

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

## <a name="6-model-advanced"></a><span data-ttu-id="64f48-306">6. Modelo avanzado</span><span class="sxs-lookup"><span data-stu-id="64f48-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="64f48-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="64f48-307">6.1.</span></span>    <span data-ttu-id="64f48-308">Modelo de detalles de datos</span><span class="sxs-lookup"><span data-stu-id="64f48-308">Model Data Insight</span></span>
<span data-ttu-id="64f48-309">Devuelve datos estadísticos sobre los datos de uso con los que se compiló este modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-309">Returns statistical data on the usage data that this model was built with.</span></span>

<span data-ttu-id="64f48-310">Disponible solo para la compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="64f48-311">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-311">HTTP Method</span></span> | <span data-ttu-id="64f48-312">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-313">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="64f48-314">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-315">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-315">Parameter Name</span></span> | <span data-ttu-id="64f48-316">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-317">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-317">modelId</span></span> |<span data-ttu-id="64f48-318">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-318">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-319">apiVersion</span></span> |<span data-ttu-id="64f48-320">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-320">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-321">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-321">Request Body</span></span> |<span data-ttu-id="64f48-322">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-322">NONE</span></span> |

<span data-ttu-id="64f48-323">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-323">**Response**:</span></span>

<span data-ttu-id="64f48-324">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-324">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-325">Los datos se devuelven como una colección de propiedades.</span><span class="sxs-lookup"><span data-stu-id="64f48-325">The data is returned as a collection of properties.</span></span>

* <span data-ttu-id="64f48-326">`feed/entry/id/content/properties/key` : contiene el nombre de propiedad.</span><span class="sxs-lookup"><span data-stu-id="64f48-326">`feed/entry/id/content/properties/key` - Holds the property name.</span></span>
* <span data-ttu-id="64f48-327">`feed/entry/id/content/properties/value` : contiene el valor de propiedad.</span><span class="sxs-lookup"><span data-stu-id="64f48-327">`feed/entry/id/content/properties/value` - Holds the property value.</span></span>

<span data-ttu-id="64f48-328">En la tabla siguiente se muestra el valor que representa cada clave.</span><span class="sxs-lookup"><span data-stu-id="64f48-328">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="64f48-329">Clave</span><span class="sxs-lookup"><span data-stu-id="64f48-329">Key</span></span> | <span data-ttu-id="64f48-330">Description</span><span class="sxs-lookup"><span data-stu-id="64f48-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="64f48-331">AvgItemLength</span></span> |<span data-ttu-id="64f48-332">Número promedio de usuarios distintos por elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="64f48-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="64f48-333">AvgUserLength</span></span> |<span data-ttu-id="64f48-334">Número promedio de usuarios distintos por usuario.</span><span class="sxs-lookup"><span data-stu-id="64f48-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="64f48-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="64f48-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="64f48-336">Número de elementos después de eliminar elementos que no se pueden modelar.</span><span class="sxs-lookup"><span data-stu-id="64f48-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="64f48-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="64f48-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="64f48-338">Número de puntos de uso después de eliminar usuarios y elementos que no se pueden modelar.</span><span class="sxs-lookup"><span data-stu-id="64f48-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="64f48-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="64f48-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="64f48-340">Número de puntos de uso después de eliminar usuarios y elementos que no se pueden modelar.</span><span class="sxs-lookup"><span data-stu-id="64f48-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="64f48-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="64f48-341">MaxItemLength</span></span> |<span data-ttu-id="64f48-342">Número de usuarios distintos para el elemento más popular.</span><span class="sxs-lookup"><span data-stu-id="64f48-342">Number of distinct users for the most popular item.</span></span> |
| <span data-ttu-id="64f48-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="64f48-343">MaxUserLength</span></span> |<span data-ttu-id="64f48-344">Número máximo de elementos distintos para un usuario.</span><span class="sxs-lookup"><span data-stu-id="64f48-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="64f48-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="64f48-345">MinItemLength</span></span> |<span data-ttu-id="64f48-346">Número máximo de usuarios distintos para un elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="64f48-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="64f48-347">MinUserLength</span></span> |<span data-ttu-id="64f48-348">Número mínimo de elementos distintos para un usuario.</span><span class="sxs-lookup"><span data-stu-id="64f48-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="64f48-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="64f48-349">RawNumberOfItems</span></span> |<span data-ttu-id="64f48-350">Número de elementos en los archivos de uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-350">Number of items in the usage files.</span></span> |
| <span data-ttu-id="64f48-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="64f48-351">RawNumberOfUsers</span></span> |<span data-ttu-id="64f48-352">Número de puntos de uso antes de cualquier eliminación.</span><span class="sxs-lookup"><span data-stu-id="64f48-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="64f48-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="64f48-353">RawNumberOfRecords</span></span> |<span data-ttu-id="64f48-354">Número de puntos de uso antes de cualquier eliminación.</span><span class="sxs-lookup"><span data-stu-id="64f48-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="64f48-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="64f48-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="64f48-356">N/D</span><span class="sxs-lookup"><span data-stu-id="64f48-356">N/A</span></span> |
| <span data-ttu-id="64f48-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="64f48-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="64f48-358">N/D</span><span class="sxs-lookup"><span data-stu-id="64f48-358">N/A</span></span> |
| <span data-ttu-id="64f48-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="64f48-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="64f48-360">N/D</span><span class="sxs-lookup"><span data-stu-id="64f48-360">N/A</span></span> |

<span data-ttu-id="64f48-361">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-361">OData XML</span></span>

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

### <a name="62----model-insight"></a><span data-ttu-id="64f48-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-362">6.2.</span></span>    <span data-ttu-id="64f48-363">Perspectiva de modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-363">Model Insight</span></span>
<span data-ttu-id="64f48-364">Devuelve información del modelo sobre la compilación activa o (si se indica) sobre una compilación concreta.</span><span class="sxs-lookup"><span data-stu-id="64f48-364">Returns model insight on the active build or (if given) on a specific build.</span></span>

<span data-ttu-id="64f48-365">Disponible solo para la compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="64f48-366">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-366">HTTP Method</span></span> | <span data-ttu-id="64f48-367">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-368">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-368">GET</span></span> |<span data-ttu-id="64f48-369">Con identificador de compilación activa:</span><span class="sxs-lookup"><span data-stu-id="64f48-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-370">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-371">Con identificador de compilación específica:</span><span class="sxs-lookup"><span data-stu-id="64f48-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-372">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-372">Parameter Name</span></span> | <span data-ttu-id="64f48-373">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-374">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-374">modelId</span></span> |<span data-ttu-id="64f48-375">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-375">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-376">buildId</span><span class="sxs-lookup"><span data-stu-id="64f48-376">buildId</span></span> |<span data-ttu-id="64f48-377">Opcional: número que identifica una compilación correcta.</span><span class="sxs-lookup"><span data-stu-id="64f48-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="64f48-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-378">apiVersion</span></span> |<span data-ttu-id="64f48-379">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-379">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-380">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-380">Request Body</span></span> |<span data-ttu-id="64f48-381">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-381">NONE</span></span> |

<span data-ttu-id="64f48-382">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-382">**Response**:</span></span>

<span data-ttu-id="64f48-383">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-383">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-384">Los datos se devuelven como una colección de propiedades.</span><span class="sxs-lookup"><span data-stu-id="64f48-384">The data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="64f48-385">En la tabla siguiente se muestra el valor que representa cada clave.</span><span class="sxs-lookup"><span data-stu-id="64f48-385">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="64f48-386">Clave</span><span class="sxs-lookup"><span data-stu-id="64f48-386">Key</span></span> | <span data-ttu-id="64f48-387">Description</span><span class="sxs-lookup"><span data-stu-id="64f48-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="64f48-388">CatalogCoverage</span></span> |<span data-ttu-id="64f48-389">¿Qué parte del catálogo puede modelarse con patrones de uso?</span><span class="sxs-lookup"><span data-stu-id="64f48-389">What part of the catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="64f48-390">El resto de los elementos necesitará características basadas en el contenido.</span><span class="sxs-lookup"><span data-stu-id="64f48-390">The rest of the items will need content-based features.</span></span> |
| <span data-ttu-id="64f48-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="64f48-391">Mpr</span></span> |<span data-ttu-id="64f48-392">Clasificación de percentil de promedio del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-392">Mean percentile ranking of the model.</span></span> <span data-ttu-id="64f48-393">Un valor bajo es mejor.</span><span class="sxs-lookup"><span data-stu-id="64f48-393">Lower is better.</span></span> |
| <span data-ttu-id="64f48-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="64f48-394">NumberOfDimensions</span></span> |<span data-ttu-id="64f48-395">Número de dimensiones usadas por el algoritmo de descomposición en factores de la matriz.</span><span class="sxs-lookup"><span data-stu-id="64f48-395">Number of dimensions used by the matrix factorization algorithm.</span></span> |

<span data-ttu-id="64f48-396">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-396">OData XML</span></span>

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

### <a name="63----get-model-sample"></a><span data-ttu-id="64f48-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="64f48-397">6.3.</span></span>    <span data-ttu-id="64f48-398">Obtener el ejemplo de modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-398">Get Model Sample</span></span>
<span data-ttu-id="64f48-399">Obtiene un ejemplo del modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-399">Gets a sample of the recommendation model.</span></span>

| <span data-ttu-id="64f48-400">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-400">HTTP Method</span></span> | <span data-ttu-id="64f48-401">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-402">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="64f48-403">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-404">Con identificador de compilación específica:</span><span class="sxs-lookup"><span data-stu-id="64f48-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="64f48-405">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-406">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-406">Parameter Name</span></span> | <span data-ttu-id="64f48-407">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-408">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-408">modelId</span></span> |<span data-ttu-id="64f48-409">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-409">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-410">apiVersion</span></span> |<span data-ttu-id="64f48-411">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-411">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-412">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-412">Request Body</span></span> |<span data-ttu-id="64f48-413">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-413">NONE</span></span> |

<span data-ttu-id="64f48-414">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-414">**Response**:</span></span>

<span data-ttu-id="64f48-415">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-415">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-416">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-416">OData XML</span></span>

<span data-ttu-id="64f48-417">Se devuelve una respuesta en formato de texto sin formato:</span><span class="sxs-lookup"><span data-stu-id="64f48-417">Response is returned in raw text format:</span></span>

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
50471eec-9aeb-4900-84d7-21567ab18546, If the Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of the Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, The Deep End of the Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, The Deep End of the Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, The Perfect Storm: A True Story of Men Against the Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: The True Story of the Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: The True Story of the Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on the Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in the Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, The Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On the Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, The Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories to Tell in the Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: The Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, The Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: The Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic the Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in the Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, The Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, The X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell the President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, The Map That Changed the World: William Smith and the Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, The Map That Changed the World: William Smith and the Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In the Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, The Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, The Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, The Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of the Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, The Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, The Perfect Storm: A True Story of Men Against the Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in the Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (The Official Guide to the X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, The Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, The Truth Is Out There (The Official Guide to the X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why the Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why the Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, The Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of the Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where the Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, The Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, The God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, The Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for the Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for the Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (The Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: The Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: The Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in the Time of Cholera (Penguin Great Books of the 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, The Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories To Tell In The Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from the Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, The Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, The Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="64f48-418">7. Reglas de negocio de modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-418">7. Model Business Rules</span></span>
<span data-ttu-id="64f48-419">Estos son los tipos de reglas admitidas:</span><span class="sxs-lookup"><span data-stu-id="64f48-419">These are the types of rules supported:</span></span>

* <span data-ttu-id="64f48-420"><strong>BlockList</strong>: le permite proporcionar una lista de elementos que no quiera que se devuelvan en los resultados de la recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-420"><strong>BlockList</strong> - BlockList enables you to provide a list of items that you do not want to return in the recommendation results.</span></span> 
* <span data-ttu-id="64f48-421"><strong>FeatureBlockList</strong>: le permite bloquear los elementos en función de los valores de sus características.</span><span class="sxs-lookup"><span data-stu-id="64f48-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you to block items based on the values of its features.</span></span>

<span data-ttu-id="64f48-422">*No envíe más de 1000 elementos en una sola regla de lista de bloqueo. Si lo hace, es posible que se agote el tiempo de espera de la llamada. Si necesita bloquear más de 1000 elementos, puede hacer varias llamadas de listas de bloqueo.*</span><span class="sxs-lookup"><span data-stu-id="64f48-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need to block more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="64f48-423"><strong>Upsale</strong>: le permite exigir los elementos que se devolverán en los resultados de la recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-423"><strong>Upsale</strong> - Upsale enables you to enforce items to return in the recommendation results.</span></span>
* <span data-ttu-id="64f48-424"><strong>WhiteList</strong>: le permite solo sugerir recomendaciones a partir de una lista de elementos.</span><span class="sxs-lookup"><span data-stu-id="64f48-424"><strong>WhiteList</strong> - White List enables you to only suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="64f48-425"><strong>FeatureWhiteList</strong>: le permite recomendar solo los elementos que tienen valores de característica específicos.</span><span class="sxs-lookup"><span data-stu-id="64f48-425"><strong>FeatureWhiteList</strong> - Feature White List enables you to only recommend items that have specific feature values.</span></span>
* <span data-ttu-id="64f48-426"><strong>PerSeedBlockList</strong>; le permite proporcionar por elemento una lista de elementos que no se pueden devolver como resultados de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you to provide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="64f48-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="64f48-427">7.1.</span></span>    <span data-ttu-id="64f48-428">Obtener reglas de modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-428">Get Model Rules</span></span>
| <span data-ttu-id="64f48-429">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-429">HTTP Method</span></span> | <span data-ttu-id="64f48-430">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-431">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="64f48-432">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-433">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-433">Parameter Name</span></span> | <span data-ttu-id="64f48-434">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-435">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-435">modelId</span></span> |<span data-ttu-id="64f48-436">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-436">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-437">apiVersion</span></span> |<span data-ttu-id="64f48-438">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-438">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-439">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-439">Request Body</span></span> |<span data-ttu-id="64f48-440">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-440">NONE</span></span> |

<span data-ttu-id="64f48-441">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-441">**Response**:</span></span>

<span data-ttu-id="64f48-442">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="64f48-443">`feed/entry/content/properties/Id` : el identificador único de esta regla.</span><span class="sxs-lookup"><span data-stu-id="64f48-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="64f48-444">`feed/entry/content/properties/Type` : el tipo de la regla.</span><span class="sxs-lookup"><span data-stu-id="64f48-444">`feed/entry/content/properties/Type` - Type of the rule.</span></span>
* <span data-ttu-id="64f48-445">`feed/entry/content/properties/Parameter` : el parámetro de regla.</span><span class="sxs-lookup"><span data-stu-id="64f48-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="64f48-446">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-446">OData XML</span></span>

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

### <a name="72----add-rule"></a><span data-ttu-id="64f48-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-447">7.2.</span></span>    <span data-ttu-id="64f48-448">Agregar regla</span><span class="sxs-lookup"><span data-stu-id="64f48-448">Add Rule</span></span>
| <span data-ttu-id="64f48-449">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-449">HTTP Method</span></span> | <span data-ttu-id="64f48-450">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-451">POST</span><span class="sxs-lookup"><span data-stu-id="64f48-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="64f48-452">ENCABEZADO</span><span class="sxs-lookup"><span data-stu-id="64f48-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="64f48-453">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-453">Parameter Name</span></span> | <span data-ttu-id="64f48-454">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-455">apiVersion</span></span> |<span data-ttu-id="64f48-456">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-456">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-457">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-457">Request Body</span></span> | |

<span data-ttu-id="64f48-458"><ins>Cada vez que se proporcionen identificadores de elemento para reglas de negocio, asegúrese de usar el Id. externo del elemento (el mismo Id. que usó en el archivo de catálogo)</ins></span><span class="sxs-lookup"><span data-stu-id="64f48-458"><ins>Whenever providing Item Ids for business rules, make sure to use the External Id of the item (the same Id that you used in the catalog file)</ins></span></span><br><span data-ttu-id="64f48-459">
<ins>Para agregar una regla BlockList:</ins></span><span class="sxs-lookup"><span data-stu-id="64f48-459">
<ins>To add a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="64f48-460"><ins>
<ins>Para agregar una regla FeatureBlockList:</ins></span><span class="sxs-lookup"><span data-stu-id="64f48-460"><ins>
<ins>To add a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="64f48-461"><ins> Para agregar una regla Upsale:</ins></span><span class="sxs-lookup"><span data-stu-id="64f48-461"><ins> To add an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="64f48-462">
<ins>Para agregar una WhiteList:</ins></span><span class="sxs-lookup"><span data-stu-id="64f48-462">
<ins>To add a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="64f48-463"><ins>
<ins>Para agregar una FeatureWhiteList:</ins></span><span class="sxs-lookup"><span data-stu-id="64f48-463"><ins>
<ins>To add a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="64f48-464"><ins> Para agregar una regla PerSeedBlockList:</ins></span><span class="sxs-lookup"><span data-stu-id="64f48-464"><ins> To add a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="64f48-465">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-465">**Response**:</span></span>

<span data-ttu-id="64f48-466">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-466">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-467">La API devuelve la regla recién creada con sus detalles.</span><span class="sxs-lookup"><span data-stu-id="64f48-467">The API returns the newly created rule with its details.</span></span> <span data-ttu-id="64f48-468">La propiedad de las reglas se puede recuperar por los siguientes medios:</span><span class="sxs-lookup"><span data-stu-id="64f48-468">The rules property can be retrieved from the following paths:</span></span>

* <span data-ttu-id="64f48-469">`feed/entry/content/properties/Id` : el identificador único de esta regla.</span><span class="sxs-lookup"><span data-stu-id="64f48-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="64f48-470">`feed/entry/content/properties/Type` : el tipo de regla, BlockList o Upsale.</span><span class="sxs-lookup"><span data-stu-id="64f48-470">`feed/entry/content/properties/Type` - Type of the rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="64f48-471">`feed/entry/content/properties/Parameter` : el parámetro de regla.</span><span class="sxs-lookup"><span data-stu-id="64f48-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="64f48-472">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-472">OData XML</span></span>

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

### <a name="73----delete-rule"></a><span data-ttu-id="64f48-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="64f48-473">7.3.</span></span>    <span data-ttu-id="64f48-474">Eliminar regla</span><span class="sxs-lookup"><span data-stu-id="64f48-474">Delete Rule</span></span>
| <span data-ttu-id="64f48-475">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-475">HTTP Method</span></span> | <span data-ttu-id="64f48-476">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-477">DELETE</span><span class="sxs-lookup"><span data-stu-id="64f48-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-478">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-479">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-479">Parameter Name</span></span> | <span data-ttu-id="64f48-480">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-481">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-481">modelId</span></span> |<span data-ttu-id="64f48-482">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-482">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-483">filterId</span><span class="sxs-lookup"><span data-stu-id="64f48-483">filterId</span></span> |<span data-ttu-id="64f48-484">Identificador único del filtro</span><span class="sxs-lookup"><span data-stu-id="64f48-484">Unique identifier of the filter</span></span> |
| <span data-ttu-id="64f48-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-485">apiVersion</span></span> |<span data-ttu-id="64f48-486">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-486">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-487">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-487">Request Body</span></span> |<span data-ttu-id="64f48-488">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-488">NONE</span></span> |

<span data-ttu-id="64f48-489">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-489">**Response**:</span></span>

<span data-ttu-id="64f48-490">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="64f48-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="64f48-491">7.4.</span></span>    <span data-ttu-id="64f48-492">Eliminar todas las reglas</span><span class="sxs-lookup"><span data-stu-id="64f48-492">Delete All Rules</span></span>
| <span data-ttu-id="64f48-493">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-493">HTTP Method</span></span> | <span data-ttu-id="64f48-494">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-495">DELETE</span><span class="sxs-lookup"><span data-stu-id="64f48-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-496">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-497">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-497">Parameter Name</span></span> | <span data-ttu-id="64f48-498">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-499">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-499">modelId</span></span> |<span data-ttu-id="64f48-500">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-500">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-501">apiVersion</span></span> |<span data-ttu-id="64f48-502">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-502">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-503">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-503">Request Body</span></span> |<span data-ttu-id="64f48-504">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-504">NONE</span></span> |

<span data-ttu-id="64f48-505">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-505">**Response**:</span></span>

<span data-ttu-id="64f48-506">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="64f48-507">8. Catálogo</span><span class="sxs-lookup"><span data-stu-id="64f48-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="64f48-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="64f48-508">8.1.</span></span>    <span data-ttu-id="64f48-509">Importar datos de catálogo</span><span class="sxs-lookup"><span data-stu-id="64f48-509">Import Catalog Data</span></span>
<span data-ttu-id="64f48-510">Si carga varios archivos de catálogo para el mismo modelo con varias llamadas, solo insertaremos los nuevos elementos de catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-510">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="64f48-511">Los elementos existentes permanecerán con los valores originales.</span><span class="sxs-lookup"><span data-stu-id="64f48-511">Existing items will remain with the original values.</span></span> <span data-ttu-id="64f48-512">Los datos del catálogo no se pueden actualizar con este método.</span><span class="sxs-lookup"><span data-stu-id="64f48-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="64f48-513">Los datos del catálogo deben seguir el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="64f48-513">The catalog data should follow the following format:</span></span>

* <span data-ttu-id="64f48-514">Sin características: `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="64f48-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="64f48-515">Con características: `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="64f48-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="64f48-516">Nota: el tamaño máximo de archivo es de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="64f48-516">Note: The maximum file size is 200MB.</span></span>

<span data-ttu-id="64f48-517">** Detalles de formato **</span><span class="sxs-lookup"><span data-stu-id="64f48-517">** Format details **</span></span>

| <span data-ttu-id="64f48-518">Nombre</span><span class="sxs-lookup"><span data-stu-id="64f48-518">Name</span></span> | <span data-ttu-id="64f48-519">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="64f48-519">Mandatory</span></span> | <span data-ttu-id="64f48-520">Tipo</span><span class="sxs-lookup"><span data-stu-id="64f48-520">Type</span></span> | <span data-ttu-id="64f48-521">Description</span><span class="sxs-lookup"><span data-stu-id="64f48-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64f48-522">Id. de elemento</span><span class="sxs-lookup"><span data-stu-id="64f48-522">Item Id</span></span> |<span data-ttu-id="64f48-523">Sí</span><span class="sxs-lookup"><span data-stu-id="64f48-523">Yes</span></span> |<span data-ttu-id="64f48-524">[A-z], [a-z], [0-9], [_] &#40;Carácter de subrayado&#41;, [-] &#40;Guion&#41;</span><span class="sxs-lookup"><span data-stu-id="64f48-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="64f48-525">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="64f48-525">Max length: 50</span></span> |<span data-ttu-id="64f48-526">Identificador único de un elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="64f48-527">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="64f48-527">Item Name</span></span> |<span data-ttu-id="64f48-528">Sí</span><span class="sxs-lookup"><span data-stu-id="64f48-528">Yes</span></span> |<span data-ttu-id="64f48-529">Cualquier carácter alfanumérico</span><span class="sxs-lookup"><span data-stu-id="64f48-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="64f48-530">Longitud máxima: 255</span><span class="sxs-lookup"><span data-stu-id="64f48-530">Max length: 255</span></span> |<span data-ttu-id="64f48-531">Nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-531">Item name.</span></span> |
| <span data-ttu-id="64f48-532">Categoría del elemento</span><span class="sxs-lookup"><span data-stu-id="64f48-532">Item Category</span></span> |<span data-ttu-id="64f48-533">Sí</span><span class="sxs-lookup"><span data-stu-id="64f48-533">Yes</span></span> |<span data-ttu-id="64f48-534">Cualquier carácter alfanumérico</span><span class="sxs-lookup"><span data-stu-id="64f48-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="64f48-535">Longitud máxima: 255</span><span class="sxs-lookup"><span data-stu-id="64f48-535">Max length: 255</span></span> |<span data-ttu-id="64f48-536">La categoría a la que pertenece este elemento (por ejemplo, Libros de cocina, Drama...); puede estar vacía.</span><span class="sxs-lookup"><span data-stu-id="64f48-536">Category to which this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="64f48-537">Description</span><span class="sxs-lookup"><span data-stu-id="64f48-537">Description</span></span> |<span data-ttu-id="64f48-538">No, a menos que haya características (pero puede estar vacía)</span><span class="sxs-lookup"><span data-stu-id="64f48-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="64f48-539">Cualquier carácter alfanumérico</span><span class="sxs-lookup"><span data-stu-id="64f48-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="64f48-540">Longitud máxima: 4000</span><span class="sxs-lookup"><span data-stu-id="64f48-540">Max length: 4000</span></span> |<span data-ttu-id="64f48-541">Descripción de este elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-541">Description of this item.</span></span> |
| <span data-ttu-id="64f48-542">Lista de características</span><span class="sxs-lookup"><span data-stu-id="64f48-542">Features list</span></span> |<span data-ttu-id="64f48-543">No</span><span class="sxs-lookup"><span data-stu-id="64f48-543">No</span></span> |<span data-ttu-id="64f48-544">Cualquier carácter alfanumérico</span><span class="sxs-lookup"><span data-stu-id="64f48-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="64f48-545">Longitud máxima: 4000; número máximo de características: 20</span><span class="sxs-lookup"><span data-stu-id="64f48-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="64f48-546">Lista de nombres de característica = valores de característica separados por coma que se pueden usar para mejorar la recomendación del modelo; consulte la sección [Temas avanzados](#2-advanced-topics) .</span><span class="sxs-lookup"><span data-stu-id="64f48-546">Comma-separated list of feature name=feature value that can be used to enhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="64f48-547">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-547">HTTP Method</span></span> | <span data-ttu-id="64f48-548">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-549">POST</span><span class="sxs-lookup"><span data-stu-id="64f48-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-550">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="64f48-551">ENCABEZADO</span><span class="sxs-lookup"><span data-stu-id="64f48-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="64f48-552">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-552">Parameter Name</span></span> | <span data-ttu-id="64f48-553">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-554">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-554">modelId</span></span> |<span data-ttu-id="64f48-555">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-555">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-556">filename</span><span class="sxs-lookup"><span data-stu-id="64f48-556">filename</span></span> |<span data-ttu-id="64f48-557">Identificador textual del catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-557">Textual identifier of the catalog.</span></span><br><span data-ttu-id="64f48-558">Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="64f48-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="64f48-559">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="64f48-559">Max length: 50</span></span> |
| <span data-ttu-id="64f48-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-560">apiVersion</span></span> |<span data-ttu-id="64f48-561">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-561">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-562">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-562">Request Body</span></span> |<span data-ttu-id="64f48-563">Ejemplo (con características):</span><span class="sxs-lookup"><span data-stu-id="64f48-563">Example (with features):</span></span><br/><span data-ttu-id="64f48-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,the book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span><span class="sxs-lookup"><span data-stu-id="64f48-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,the book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="64f48-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span><span class="sxs-lookup"><span data-stu-id="64f48-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="64f48-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="64f48-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="64f48-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,the book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span><span class="sxs-lookup"><span data-stu-id="64f48-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,the book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="64f48-568">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-568">**Response**:</span></span>

<span data-ttu-id="64f48-569">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-569">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-570">La API devuelve un informe de la importación.</span><span class="sxs-lookup"><span data-stu-id="64f48-570">The API returns a report of the import.</span></span>

* <span data-ttu-id="64f48-571">`feed\entry\content\properties\LineCount` : número de líneas aceptadas.</span><span class="sxs-lookup"><span data-stu-id="64f48-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="64f48-572">`feed\entry\content\properties\ErrorCount` : número de líneas que no se insertaron debido a un error.</span><span class="sxs-lookup"><span data-stu-id="64f48-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="64f48-573">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-573">OData XML</span></span>

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

### <a name="82----get-catalog"></a><span data-ttu-id="64f48-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-574">8.2.</span></span>    <span data-ttu-id="64f48-575">Obtener catálogo</span><span class="sxs-lookup"><span data-stu-id="64f48-575">Get Catalog</span></span>
<span data-ttu-id="64f48-576">Recupera todos los elementos del catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="64f48-577">El catálogo se recuperará de página en página.</span><span class="sxs-lookup"><span data-stu-id="64f48-577">The catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="64f48-578">Si desea obtener elementos en un índice determinado, puede utilizar el parámetro de OData $skip.</span><span class="sxs-lookup"><span data-stu-id="64f48-578">If you want to get items at a particular index, you can use the $skip odata parameter.</span></span> <span data-ttu-id="64f48-579">Por ejemplo, si desea obtener elementos a partir de la posición 100, agregue el parámetro $skip=100 a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="64f48-579">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span></span>

| <span data-ttu-id="64f48-580">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-580">HTTP Method</span></span> | <span data-ttu-id="64f48-581">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-582">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-583">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-584">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-584">Parameter Name</span></span> | <span data-ttu-id="64f48-585">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-586">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-586">modelId</span></span> |<span data-ttu-id="64f48-587">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-587">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-588">apiVersion</span></span> |<span data-ttu-id="64f48-589">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-589">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-590">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-590">Request Body</span></span> |<span data-ttu-id="64f48-591">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-591">NONE</span></span> |

<span data-ttu-id="64f48-592">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-592">**Response**:</span></span>

<span data-ttu-id="64f48-593">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-593">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-594">La respuesta incluye una entrada por cada elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-594">The response includes one entry per catalog item.</span></span> <span data-ttu-id="64f48-595">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-595">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-596">`feed/entry/content/properties/ExternalId` : identificador externo de elemento de catálogo, proporcionado por el cliente.</span><span class="sxs-lookup"><span data-stu-id="64f48-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, the one provided by the customer.</span></span>
* <span data-ttu-id="64f48-597">`feed/entry/content/properties/InternalId` : identificador interno de elemento de catálogo, que ha generado las Recomendaciones de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="64f48-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="64f48-598">`feed/entry/content/properties/Name` : nombre de elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="64f48-599">`feed/entry/content/properties/Category` : categoría de elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="64f48-600">`feed/entry/content/properties/Description` : descripción de elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="64f48-601">`feed/entry/content/properties/Metadata` : metadatos de elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="64f48-602">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-602">OData XML</span></span>

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
                <d:Name m:type="Edm.String">The Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="64f48-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="64f48-603">8.3.</span></span>    <span data-ttu-id="64f48-604">Obtener elementos de catálogo por token</span><span class="sxs-lookup"><span data-stu-id="64f48-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="64f48-605">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-605">HTTP Method</span></span> | <span data-ttu-id="64f48-606">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-607">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-608">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-609">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-609">Parameter Name</span></span> | <span data-ttu-id="64f48-610">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-611">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-611">modelId</span></span> |<span data-ttu-id="64f48-612">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-612">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-613">token</span><span class="sxs-lookup"><span data-stu-id="64f48-613">token</span></span> |<span data-ttu-id="64f48-614">Token del nombre de elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-614">Token of the catalog item’s name.</span></span> <span data-ttu-id="64f48-615">Debe contener al menos 3 caracteres.</span><span class="sxs-lookup"><span data-stu-id="64f48-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="64f48-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-616">apiVersion</span></span> |<span data-ttu-id="64f48-617">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-617">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-618">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-618">Request Body</span></span> |<span data-ttu-id="64f48-619">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-619">NONE</span></span> |

<span data-ttu-id="64f48-620">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-620">**Response**:</span></span>

<span data-ttu-id="64f48-621">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-621">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-622">La respuesta incluye una entrada por cada elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-622">The response includes one entry per catalog item.</span></span> <span data-ttu-id="64f48-623">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-623">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-624">`feed/entry/content/properties/InternalId` : identificador interno de elemento de catálogo, que ha generado las Recomendaciones de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="64f48-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="64f48-625">`feed/entry/content/properties/Name` : nombre de elemento de catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="64f48-626">`feed/entry/content/properties/Rating`: (para un uso futuro)</span><span class="sxs-lookup"><span data-stu-id="64f48-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="64f48-627">`feed/entry/content/properties/Reasoning`: (para un uso futuro)</span><span class="sxs-lookup"><span data-stu-id="64f48-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="64f48-628">`feed/entry/content/properties/Metadata`: (para un uso futuro)</span><span class="sxs-lookup"><span data-stu-id="64f48-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="64f48-629">`feed/entry/content/properties/FormattedRating` : (para un uso futuro)</span><span class="sxs-lookup"><span data-stu-id="64f48-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="64f48-630">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-630">OData XML</span></span>

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

## <a name="9-usage-data"></a><span data-ttu-id="64f48-631">9. Datos de uso</span><span class="sxs-lookup"><span data-stu-id="64f48-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="64f48-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="64f48-632">9.1.</span></span>    <span data-ttu-id="64f48-633">Importar datos de uso</span><span class="sxs-lookup"><span data-stu-id="64f48-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="64f48-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="64f48-634">9.1.1.</span></span> <span data-ttu-id="64f48-635">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="64f48-635">Uploading File</span></span>
<span data-ttu-id="64f48-636">En esta sección se muestra cómo cargar datos de uso mediante un archivo.</span><span class="sxs-lookup"><span data-stu-id="64f48-636">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="64f48-637">Puede llamar a esta API varias veces con datos de uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="64f48-638">Todos los datos de uso se guardarán para todas las llamadas.</span><span class="sxs-lookup"><span data-stu-id="64f48-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="64f48-639">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-639">HTTP Method</span></span> | <span data-ttu-id="64f48-640">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-641">POST</span><span class="sxs-lookup"><span data-stu-id="64f48-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-642">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-643">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-643">Parameter Name</span></span> | <span data-ttu-id="64f48-644">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-645">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-645">modelId</span></span> |<span data-ttu-id="64f48-646">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-646">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-647">filename</span><span class="sxs-lookup"><span data-stu-id="64f48-647">filename</span></span> |<span data-ttu-id="64f48-648">Identificador textual del catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-648">Textual identifier of the catalog.</span></span><br><span data-ttu-id="64f48-649">Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="64f48-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="64f48-650">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="64f48-650">Max length: 50</span></span> |
| <span data-ttu-id="64f48-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-651">apiVersion</span></span> |<span data-ttu-id="64f48-652">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-652">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-653">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-653">Request Body</span></span> |<span data-ttu-id="64f48-654">Datos de uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-654">Usage data.</span></span> <span data-ttu-id="64f48-655">Formato:</span><span class="sxs-lookup"><span data-stu-id="64f48-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="64f48-656">Nombre</span><span class="sxs-lookup"><span data-stu-id="64f48-656">Name</span></span></th><th><span data-ttu-id="64f48-657">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="64f48-657">Mandatory</span></span></th><th><span data-ttu-id="64f48-658">Tipo</span><span class="sxs-lookup"><span data-stu-id="64f48-658">Type</span></span></th><th><span data-ttu-id="64f48-659">Description</span><span class="sxs-lookup"><span data-stu-id="64f48-659">Description</span></span></th></tr><tr><td><span data-ttu-id="64f48-660">Id. de usuario</span><span class="sxs-lookup"><span data-stu-id="64f48-660">User Id</span></span></td><td><span data-ttu-id="64f48-661">Sí</span><span class="sxs-lookup"><span data-stu-id="64f48-661">Yes</span></span></td><td><span data-ttu-id="64f48-662">[A-z], [a-z], [0-9], [_] &#40;Carácter de subrayado&#41;, [-] &#40;Guion&#41;</span><span class="sxs-lookup"><span data-stu-id="64f48-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="64f48-663">Longitud máxima: 255</span><span class="sxs-lookup"><span data-stu-id="64f48-663">Max length: 255</span></span> </td><td><span data-ttu-id="64f48-664">Identificador único de un usuario.</span><span class="sxs-lookup"><span data-stu-id="64f48-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="64f48-665">Id. de elemento</span><span class="sxs-lookup"><span data-stu-id="64f48-665">Item Id</span></span></td><td><span data-ttu-id="64f48-666">Sí</span><span class="sxs-lookup"><span data-stu-id="64f48-666">Yes</span></span></td><td><span data-ttu-id="64f48-667">[A-z], [a-z], [0-9], [&#95;] &#40;Carácter de subrayado&#41;, [-] &#40;Guion&#41;</span><span class="sxs-lookup"><span data-stu-id="64f48-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="64f48-668">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="64f48-668">Max length: 50</span></span></td><td><span data-ttu-id="64f48-669">Identificador único de un elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="64f48-670">Hora</span><span class="sxs-lookup"><span data-stu-id="64f48-670">Time</span></span></td><td><span data-ttu-id="64f48-671">No</span><span class="sxs-lookup"><span data-stu-id="64f48-671">No</span></span></td><td><span data-ttu-id="64f48-672">La fecha en este formato: AAAA/MM/DDTHH:MM:SS (por ejemplo, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="64f48-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="64f48-673">Hora de los datos.</span><span class="sxs-lookup"><span data-stu-id="64f48-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="64f48-674">Evento</span><span class="sxs-lookup"><span data-stu-id="64f48-674">Event</span></span></td><td><span data-ttu-id="64f48-675">No, si se suministra también se debe colocar la fecha</span><span class="sxs-lookup"><span data-stu-id="64f48-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="64f48-676">Uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="64f48-676">One of the following:</span></span><br><span data-ttu-id="64f48-677">• Click</span><span class="sxs-lookup"><span data-stu-id="64f48-677">• Click</span></span><br><span data-ttu-id="64f48-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="64f48-678">• RecommendationClick</span></span><br><span data-ttu-id="64f48-679">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="64f48-679">•    AddShopCart</span></span><br><span data-ttu-id="64f48-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="64f48-680">• RemoveShopCart</span></span><br><span data-ttu-id="64f48-681">• compra</span><span class="sxs-lookup"><span data-stu-id="64f48-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="64f48-682">Tamaño de archivo máximo: 200 MB</span><span class="sxs-lookup"><span data-stu-id="64f48-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="64f48-683">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="64f48-684">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-684">**Response**:</span></span>

<span data-ttu-id="64f48-685">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="64f48-686">`Feed\entry\content\properties\LineCount` : número de líneas aceptadas.</span><span class="sxs-lookup"><span data-stu-id="64f48-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="64f48-687">`Feed\entry\content\properties\ErrorCount` : número de líneas que no se insertaron debido a un error.</span><span class="sxs-lookup"><span data-stu-id="64f48-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="64f48-688">`Feed\entry\content\properties\FileId` : identificador de archivo.</span><span class="sxs-lookup"><span data-stu-id="64f48-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="64f48-689">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-689">OData XML</span></span>

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


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="64f48-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-690">9.1.2.</span></span> <span data-ttu-id="64f48-691">Uso de la adquisición de datos</span><span class="sxs-lookup"><span data-stu-id="64f48-691">Using Data Acquisition</span></span>
<span data-ttu-id="64f48-692">En esta sección se muestra cómo enviar eventos en tiempo real a las recomendaciones de Aprendizaje automático de Azure, normalmente desde su sitio web.</span><span class="sxs-lookup"><span data-stu-id="64f48-692">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="64f48-693">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-693">HTTP Method</span></span> | <span data-ttu-id="64f48-694">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-695">POST</span><span class="sxs-lookup"><span data-stu-id="64f48-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="64f48-696">ENCABEZADO</span><span class="sxs-lookup"><span data-stu-id="64f48-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="64f48-697">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-697">Parameter Name</span></span> | <span data-ttu-id="64f48-698">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-699">apiVersion</span></span> |<span data-ttu-id="64f48-700">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-700">1.0</span></span> |
| <span data-ttu-id="64f48-701">Request body</span><span class="sxs-lookup"><span data-stu-id="64f48-701">Request body</span></span> |<span data-ttu-id="64f48-702">Entrada de datos de eventos para cada evento que va a enviar.</span><span class="sxs-lookup"><span data-stu-id="64f48-702">Event data entry for each event you want to send.</span></span> <span data-ttu-id="64f48-703">Debe enviar para la misma sesión de usuario o explorador el mismo identificador en el campo SessionId.</span><span class="sxs-lookup"><span data-stu-id="64f48-703">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="64f48-704">(Vea el ejemplo del cuerpo de evento aparece a continuación).</span><span class="sxs-lookup"><span data-stu-id="64f48-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="64f48-705">Ejemplo para evento 'Click':</span><span class="sxs-lookup"><span data-stu-id="64f48-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="64f48-706">Ejemplo para evento 'RecommendationClick':</span><span class="sxs-lookup"><span data-stu-id="64f48-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="64f48-707">Ejemplo para evento 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="64f48-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="64f48-708">Ejemplo para evento 'RemoveShopCart':</span><span class="sxs-lookup"><span data-stu-id="64f48-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="64f48-709">Ejemplo para el evento “Purchase”:</span><span class="sxs-lookup"><span data-stu-id="64f48-709">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="64f48-710">Ejemplo con envío de 2 eventos, 'Click' y 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="64f48-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="64f48-711">**Respuesta**: código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="64f48-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-712">9.2.</span></span>    <span data-ttu-id="64f48-713">Mostrar archivos de uso de modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-713">List Model Usage Files</span></span>
<span data-ttu-id="64f48-714">Recupera los metadatos de todos los archivos de uso de modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="64f48-715">Los archivos de uso se recuperarán de página en página.</span><span class="sxs-lookup"><span data-stu-id="64f48-715">The usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="64f48-716">Cada página contiene 100 elementos.</span><span class="sxs-lookup"><span data-stu-id="64f48-716">Each page containes 100 items.</span></span> <span data-ttu-id="64f48-717">Si desea obtener elementos en un índice determinado, puede utilizar el parámetro de OData $skip.</span><span class="sxs-lookup"><span data-stu-id="64f48-717">If you want to get items at a particular index, you can use the $skip odata parameter.</span></span> <span data-ttu-id="64f48-718">Por ejemplo, si desea obtener elementos a partir de la posición 100, agregue el parámetro $skip=100 a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="64f48-718">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span></span>

| <span data-ttu-id="64f48-719">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-719">HTTP Method</span></span> | <span data-ttu-id="64f48-720">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-721">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-722">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-723">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-723">Parameter Name</span></span> | <span data-ttu-id="64f48-724">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="64f48-725">forModelId</span></span> |<span data-ttu-id="64f48-726">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-726">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-727">apiVersion</span></span> |<span data-ttu-id="64f48-728">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-728">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-729">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-729">Request Body</span></span> |<span data-ttu-id="64f48-730">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-730">NONE</span></span> |

<span data-ttu-id="64f48-731">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-731">**Response**:</span></span>

<span data-ttu-id="64f48-732">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-732">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-733">La respuesta incluye una entrada por archivo de uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-733">The response includes one entry per usage file.</span></span> <span data-ttu-id="64f48-734">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-734">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-735">`feed\entry\content\properties\Id`: id. de archivo de uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="64f48-736">`feed\entry\content\properties\Length`: longitud del archivo uso en MB.</span><span class="sxs-lookup"><span data-stu-id="64f48-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="64f48-737">`feed\entry\content\properties\DateModified` : fecha en que se creó el archivo de uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-737">`feed\entry\content\properties\DateModified` - Date when the usage file was created.</span></span>
* <span data-ttu-id="64f48-738">`feed\entry\content\properties\UseInModel` : si el archivo de uso se emplea en el modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-738">`feed\entry\content\properties\UseInModel` - Whether the usage file is used in the model.</span></span>

<span data-ttu-id="64f48-739">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-739">OData XML</span></span>

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

### <a name="93----get-usage-statistics"></a><span data-ttu-id="64f48-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="64f48-740">9.3.</span></span>    <span data-ttu-id="64f48-741">Obtener estadísticas de uso</span><span class="sxs-lookup"><span data-stu-id="64f48-741">Get Usage Statistics</span></span>
<span data-ttu-id="64f48-742">Obtiene estadísticas de uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-742">Gets usage statistics.</span></span>

| <span data-ttu-id="64f48-743">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-743">HTTP Method</span></span> | <span data-ttu-id="64f48-744">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-745">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-746">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-747">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-747">Parameter Name</span></span> | <span data-ttu-id="64f48-748">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-749">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-749">modelId</span></span> |<span data-ttu-id="64f48-750">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-750">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-751">startDate</span><span class="sxs-lookup"><span data-stu-id="64f48-751">startDate</span></span> |<span data-ttu-id="64f48-752">Fecha de inicio.</span><span class="sxs-lookup"><span data-stu-id="64f48-752">Start date.</span></span> <span data-ttu-id="64f48-753">Formato: aaaa/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="64f48-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="64f48-754">endDate</span><span class="sxs-lookup"><span data-stu-id="64f48-754">endDate</span></span> |<span data-ttu-id="64f48-755">Fecha de fin.</span><span class="sxs-lookup"><span data-stu-id="64f48-755">End date.</span></span> <span data-ttu-id="64f48-756">Formato: aaaa/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="64f48-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="64f48-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="64f48-757">eventTypes</span></span> |<span data-ttu-id="64f48-758">Cadena de tipos de eventos separados por coma o null para obtener todos los eventos.</span><span class="sxs-lookup"><span data-stu-id="64f48-758">Comma-separated string of event types or null to get all events</span></span> |
| <span data-ttu-id="64f48-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-759">apiVersion</span></span> |<span data-ttu-id="64f48-760">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-760">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-761">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-761">Request Body</span></span> |<span data-ttu-id="64f48-762">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-762">NONE</span></span> |

<span data-ttu-id="64f48-763">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-763">**Response**:</span></span>

<span data-ttu-id="64f48-764">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-764">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-765">Una colección de elementos de clave y valor.</span><span class="sxs-lookup"><span data-stu-id="64f48-765">A collection of key/value elements.</span></span> <span data-ttu-id="64f48-766">Cada uno contiene la suma de eventos para un tipo de evento concreto, agrupados por hora.</span><span class="sxs-lookup"><span data-stu-id="64f48-766">Each one contains the sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="64f48-767">`feed\entry[i]\content\properties\Key` : contiene el tiempo (agrupado por hora) y el tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="64f48-767">`feed\entry[i]\content\properties\Key` - Contains the time (grouped by hour) and the event type.</span></span>
* <span data-ttu-id="64f48-768">`feed\entry[i]\content\properties\Value` : recuento total de eventos.</span><span class="sxs-lookup"><span data-stu-id="64f48-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="64f48-769">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-769">OData XML</span></span>

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

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="64f48-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="64f48-770">9.4.</span></span>    <span data-ttu-id="64f48-771">Obtener ejemplo de archivo de uso</span><span class="sxs-lookup"><span data-stu-id="64f48-771">Get Usage File Sample</span></span>
<span data-ttu-id="64f48-772">Recupera los primeros 2 KB de contenido de archivos de uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-772">Retrieves the first 2KB of usage file content.</span></span>

| <span data-ttu-id="64f48-773">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-773">HTTP Method</span></span> | <span data-ttu-id="64f48-774">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-775">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-776">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-777">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-777">Parameter Name</span></span> | <span data-ttu-id="64f48-778">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-779">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-779">modelId</span></span> |<span data-ttu-id="64f48-780">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-780">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-781">fileId</span><span class="sxs-lookup"><span data-stu-id="64f48-781">fileId</span></span> |<span data-ttu-id="64f48-782">Identificador único del archivo de uso de modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-782">Unique identifier of the model usage file</span></span> |
| <span data-ttu-id="64f48-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-783">apiVersion</span></span> |<span data-ttu-id="64f48-784">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-784">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-785">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-785">Request Body</span></span> |<span data-ttu-id="64f48-786">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-786">NONE</span></span> |

<span data-ttu-id="64f48-787">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-787">**Response**:</span></span>

<span data-ttu-id="64f48-788">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-788">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-789">Se devuelve una respuesta en formato de texto sin formato:</span><span class="sxs-lookup"><span data-stu-id="64f48-789">Response is returned in raw text format:</span></span>

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


### <a name="95----get-model-usage-file"></a><span data-ttu-id="64f48-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="64f48-790">9.5.</span></span>    <span data-ttu-id="64f48-791">Obtener el archivo de uso de modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-791">Get Model Usage File</span></span>
<span data-ttu-id="64f48-792">Recupera el contenido completo del archivo de uso.</span><span class="sxs-lookup"><span data-stu-id="64f48-792">Retrieves the full content of the usage file.</span></span>

| <span data-ttu-id="64f48-793">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-793">HTTP Method</span></span> | <span data-ttu-id="64f48-794">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-795">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-796">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-797">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-797">Parameter Name</span></span> | <span data-ttu-id="64f48-798">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-799">mId</span><span class="sxs-lookup"><span data-stu-id="64f48-799">mid</span></span> |<span data-ttu-id="64f48-800">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-800">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-801">fid</span><span class="sxs-lookup"><span data-stu-id="64f48-801">fid</span></span> |<span data-ttu-id="64f48-802">Identificador único del archivo de uso de modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-802">Unique identifier of the model usage file</span></span> |
| <span data-ttu-id="64f48-803">descargar</span><span class="sxs-lookup"><span data-stu-id="64f48-803">download</span></span> |<span data-ttu-id="64f48-804">1</span><span class="sxs-lookup"><span data-stu-id="64f48-804">1</span></span> |
| <span data-ttu-id="64f48-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-805">apiVersion</span></span> |<span data-ttu-id="64f48-806">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-806">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-807">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-807">Request Body</span></span> |<span data-ttu-id="64f48-808">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-808">NONE</span></span> |

<span data-ttu-id="64f48-809">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-809">**Response**:</span></span>

<span data-ttu-id="64f48-810">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-810">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-811">Se devuelve una respuesta en formato de texto sin formato:</span><span class="sxs-lookup"><span data-stu-id="64f48-811">Response is returned in raw text format:</span></span>

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

### <a name="96----delete-usage-file"></a><span data-ttu-id="64f48-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="64f48-812">9.6.</span></span>    <span data-ttu-id="64f48-813">Eliminar archivo de uso</span><span class="sxs-lookup"><span data-stu-id="64f48-813">Delete Usage File</span></span>
<span data-ttu-id="64f48-814">Elimina el archivo de uso del modelo especificado.</span><span class="sxs-lookup"><span data-stu-id="64f48-814">Deletes the specified model usage file.</span></span>

| <span data-ttu-id="64f48-815">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-815">HTTP Method</span></span> | <span data-ttu-id="64f48-816">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-817">DELETE</span><span class="sxs-lookup"><span data-stu-id="64f48-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-818">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-819">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-819">Parameter Name</span></span> | <span data-ttu-id="64f48-820">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-821">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-821">modelId</span></span> |<span data-ttu-id="64f48-822">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-822">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-823">fileId</span><span class="sxs-lookup"><span data-stu-id="64f48-823">fileId</span></span> |<span data-ttu-id="64f48-824">Identificador único del archivo que se va a eliminar</span><span class="sxs-lookup"><span data-stu-id="64f48-824">Unique identifier of the file to be deleted</span></span> |
| <span data-ttu-id="64f48-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-825">apiVersion</span></span> |<span data-ttu-id="64f48-826">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-826">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-827">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-827">Request Body</span></span> |<span data-ttu-id="64f48-828">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-828">NONE</span></span> |

<span data-ttu-id="64f48-829">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-829">**Response**:</span></span>

<span data-ttu-id="64f48-830">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="64f48-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="64f48-831">9.7.</span></span>    <span data-ttu-id="64f48-832">Eliminar todos los archivos de uso</span><span class="sxs-lookup"><span data-stu-id="64f48-832">Delete All Usage Files</span></span>
<span data-ttu-id="64f48-833">Elimina todos los archivos de uso del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="64f48-834">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-834">HTTP Method</span></span> | <span data-ttu-id="64f48-835">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-836">DELETE</span><span class="sxs-lookup"><span data-stu-id="64f48-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-837">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-838">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-838">Parameter Name</span></span> | <span data-ttu-id="64f48-839">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-840">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-840">modelId</span></span> |<span data-ttu-id="64f48-841">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-841">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-842">apiVersion</span></span> |<span data-ttu-id="64f48-843">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-843">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-844">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-844">Request Body</span></span> |<span data-ttu-id="64f48-845">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-845">NONE</span></span> |

<span data-ttu-id="64f48-846">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-846">**Response**:</span></span>

<span data-ttu-id="64f48-847">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="64f48-848">10. Características</span><span class="sxs-lookup"><span data-stu-id="64f48-848">10. Features</span></span>
<span data-ttu-id="64f48-849">En esta sección se muestra cómo recuperar información de características, como las funciones importadas y sus valores, su rango, y cuándo se ha asignado este rango.</span><span class="sxs-lookup"><span data-stu-id="64f48-849">This section shows how to retrieve feature information, such as the imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="64f48-850">Las características se importan como parte de los datos del catálogo y luego su rango se asocia cuando se realiza una compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="64f48-850">Features are imported as part of the catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="64f48-851">El rango de las características puede cambiar según el patrón de los datos de uso y el tipo de elementos.</span><span class="sxs-lookup"><span data-stu-id="64f48-851">Feature rank can change according to the pattern of usage data and type of items.</span></span> <span data-ttu-id="64f48-852">Pero para que el uso y los elementos sean coherentes, el rango debe tener solo pequeñas fluctuaciones.</span><span class="sxs-lookup"><span data-stu-id="64f48-852">But for consistent usage/items, the rank should have only small fluctuations.</span></span>
<span data-ttu-id="64f48-853">El rango de características es un número no negativo.</span><span class="sxs-lookup"><span data-stu-id="64f48-853">The rank of features is a non-negative number.</span></span> <span data-ttu-id="64f48-854">El número 0 significa que la característica no fue clasificada (sucede si se invoca esta API antes de completar la primera compilación de rango).</span><span class="sxs-lookup"><span data-stu-id="64f48-854">The  number 0 means that the feature was not ranked (happens if you invoke this API prior to the completion of the first rank build).</span></span> <span data-ttu-id="64f48-855">La fecha en que se atribuye el rango se conoce como la actualización de la puntuación.</span><span class="sxs-lookup"><span data-stu-id="64f48-855">The date at which the rank was attributed is called the score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="64f48-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="64f48-856">10.1.</span></span> <span data-ttu-id="64f48-857">Obtener información de características (para la última compilación de rango)</span><span class="sxs-lookup"><span data-stu-id="64f48-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="64f48-858">Recupera la información de características, incluida la clasificación de la última compilación correcta de rango.</span><span class="sxs-lookup"><span data-stu-id="64f48-858">Retrieves the feature information, including ranking, for the last successful rank build.</span></span>

| <span data-ttu-id="64f48-859">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-859">HTTP Method</span></span> | <span data-ttu-id="64f48-860">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-861">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-862">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-863">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-863">Parameter Name</span></span> | <span data-ttu-id="64f48-864">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-865">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-865">modelId</span></span> |<span data-ttu-id="64f48-866">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-866">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="64f48-867">samplingSize</span></span> |<span data-ttu-id="64f48-868">Número de valores que se incluirán para cada característica de acuerdo con los datos presentes en el catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-868">Number of values to include for each feature according to the data present in the catalog.</span></span> <br/><span data-ttu-id="64f48-869">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="64f48-869">Possible values are:</span></span><br> <span data-ttu-id="64f48-870">-1 - Todas las muestras.</span><span class="sxs-lookup"><span data-stu-id="64f48-870">-1 - All samples.</span></span> <br><span data-ttu-id="64f48-871">0: sin muestreo.</span><span class="sxs-lookup"><span data-stu-id="64f48-871">0 - No sampling.</span></span> <br><span data-ttu-id="64f48-872">N: se devuelven N muestras para cada nombre de característica.</span><span class="sxs-lookup"><span data-stu-id="64f48-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="64f48-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-873">apiVersion</span></span> |<span data-ttu-id="64f48-874">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-874">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-875">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-875">Request Body</span></span> |<span data-ttu-id="64f48-876">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-876">NONE</span></span> |

<span data-ttu-id="64f48-877">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-877">**Response**:</span></span>

<span data-ttu-id="64f48-878">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-878">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-879">La respuesta contiene una lista de entradas de información de características.</span><span class="sxs-lookup"><span data-stu-id="64f48-879">The response contains a list of feature info entries.</span></span> <span data-ttu-id="64f48-880">Cada entrada contiene:</span><span class="sxs-lookup"><span data-stu-id="64f48-880">Each entry contains:</span></span>

* <span data-ttu-id="64f48-881">`feed/entry/content/m:properties/d:Name` : nombre de la característica.</span><span class="sxs-lookup"><span data-stu-id="64f48-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="64f48-882">`feed/entry/content/m:properties/d:RankUpdateDate`:-fecha en la que se asignó el rango a esta característica, también conocida como</span><span class="sxs-lookup"><span data-stu-id="64f48-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span></span> <span data-ttu-id="64f48-883">característica de actualización de puntuación.</span><span class="sxs-lookup"><span data-stu-id="64f48-883">score freshness feature.</span></span> <span data-ttu-id="64f48-884">Una fecha histórica ('0001-01-01T00:00:00') significa que no se ha realizado ninguna compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="64f48-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="64f48-885">`feed/entry/content/m:properties/d:Rank`: rango de característica (flotante).</span><span class="sxs-lookup"><span data-stu-id="64f48-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="64f48-886">Un rango de 2.0 para arriba se considera una buena característica.</span><span class="sxs-lookup"><span data-stu-id="64f48-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="64f48-887">`feed/entry/content/m:properties/d:SampleValues` : lista de valores separados por coma hasta el tamaño de muestreo solicitado.</span><span class="sxs-lookup"><span data-stu-id="64f48-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span></span>

<span data-ttu-id="64f48-888">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get the features of a model</subtitle>
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

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="64f48-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-889">10.2.</span></span> <span data-ttu-id="64f48-890">Obtener información de características (para una compilación de rango específica)</span><span class="sxs-lookup"><span data-stu-id="64f48-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="64f48-891">Recupera la información de características, incluida la clasificación de una compilación de rango específica.</span><span class="sxs-lookup"><span data-stu-id="64f48-891">Retrieves the feature information, including the ranking for a specific rank build.</span></span>

| <span data-ttu-id="64f48-892">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-892">HTTP Method</span></span> | <span data-ttu-id="64f48-893">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-894">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-895">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-896">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-896">Parameter Name</span></span> | <span data-ttu-id="64f48-897">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-898">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-898">modelId</span></span> |<span data-ttu-id="64f48-899">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-899">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="64f48-900">samplingSize</span></span> |<span data-ttu-id="64f48-901">Número de valores que se incluirán para cada característica de acuerdo con los datos presentes en el catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-901">Number of values to include for each feature according to the data present in the catalog.</span></span><br/> <span data-ttu-id="64f48-902">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="64f48-902">Possible values are:</span></span><br> <span data-ttu-id="64f48-903">-1 - Todas las muestras.</span><span class="sxs-lookup"><span data-stu-id="64f48-903">-1 - All samples.</span></span> <br><span data-ttu-id="64f48-904">0: sin muestreo.</span><span class="sxs-lookup"><span data-stu-id="64f48-904">0 - No sampling.</span></span> <br><span data-ttu-id="64f48-905">N: se devuelven N muestras para cada nombre de característica.</span><span class="sxs-lookup"><span data-stu-id="64f48-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="64f48-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="64f48-906">rankBuildId</span></span> |<span data-ttu-id="64f48-907">Identificador único de la compilación de rango o -1 para la última compilación de rango</span><span class="sxs-lookup"><span data-stu-id="64f48-907">Unique identifier of the rank build or -1 for the last rank build</span></span> |
| <span data-ttu-id="64f48-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-908">apiVersion</span></span> |<span data-ttu-id="64f48-909">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-909">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-910">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-910">Request Body</span></span> |<span data-ttu-id="64f48-911">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-911">NONE</span></span> |

<span data-ttu-id="64f48-912">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-912">**Response**:</span></span>

<span data-ttu-id="64f48-913">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-913">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-914">La respuesta contiene una lista de entradas de información de características.</span><span class="sxs-lookup"><span data-stu-id="64f48-914">The response contains a list of feature info entries.</span></span> <span data-ttu-id="64f48-915">Cada entrada contiene:</span><span class="sxs-lookup"><span data-stu-id="64f48-915">Each entry contains:</span></span>

* <span data-ttu-id="64f48-916">`feed/entry/content/m:properties/d:Name` : nombre de la característica.</span><span class="sxs-lookup"><span data-stu-id="64f48-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="64f48-917">`feed/entry/content/m:properties/d:RankUpdateDate`:-fecha en la que se asignó el rango a esta característica, también conocida como</span><span class="sxs-lookup"><span data-stu-id="64f48-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span></span> <span data-ttu-id="64f48-918">característica de actualización de puntuación.</span><span class="sxs-lookup"><span data-stu-id="64f48-918">score freshness feature.</span></span> <span data-ttu-id="64f48-919">Una fecha histórica ('0001-01-01T00:00:00') significa que no se ha realizado ninguna compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="64f48-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="64f48-920">`feed/entry/content/m:properties/d:Rank`: rango de característica (flotante).</span><span class="sxs-lookup"><span data-stu-id="64f48-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="64f48-921">Un rango de 2.0 para arriba se considera una buena característica.</span><span class="sxs-lookup"><span data-stu-id="64f48-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="64f48-922">`feed/entry/content/m:properties/d:SampleValues` : lista de valores separados por coma hasta el tamaño de muestreo solicitado.</span><span class="sxs-lookup"><span data-stu-id="64f48-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span></span>

<span data-ttu-id="64f48-923">OData</span><span class="sxs-lookup"><span data-stu-id="64f48-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get the features of a model</subtitle>
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


## <a name="11-build"></a><span data-ttu-id="64f48-924">11. Compilación</span><span class="sxs-lookup"><span data-stu-id="64f48-924">11. Build</span></span>
  <span data-ttu-id="64f48-925">En esta sección se explican las diferentes API relacionadas con compilaciones.</span><span class="sxs-lookup"><span data-stu-id="64f48-925">This section explains the different APIs related to builds.</span></span> <span data-ttu-id="64f48-926">Hay tres tipos de compilación: una compilación de recomendación, una compilación de rango y una compilación FBT (artículos que con frecuencia se compran juntos).</span><span class="sxs-lookup"><span data-stu-id="64f48-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="64f48-927">El objetivo de la compilación de recomendación es generar un modelo de recomendación que se usa en las predicciones.</span><span class="sxs-lookup"><span data-stu-id="64f48-927">The recommendation build's purpose is to generate a recommendation model used for predictions.</span></span> <span data-ttu-id="64f48-928">Las predicciones (para este tipo de compilación) se presentan en dos modos:</span><span class="sxs-lookup"><span data-stu-id="64f48-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="64f48-929">I2I - también conocida como</span><span class="sxs-lookup"><span data-stu-id="64f48-929">I2I - a.k.a.</span></span> <span data-ttu-id="64f48-930">Recomendaciones de elemento a elemento: dado un elemento o una lista de elementos, esta opción predirá una lista de elementos que pueden ser de gran interés.</span><span class="sxs-lookup"><span data-stu-id="64f48-930">Item to Item recommendations - given an item or a list of items this option will predict a list of items that are likely to be of high interest.</span></span>
* <span data-ttu-id="64f48-931">U2I - también conocida como</span><span class="sxs-lookup"><span data-stu-id="64f48-931">U2I - a.k.a.</span></span> <span data-ttu-id="64f48-932">de usuario (y opcionalmente una lista de elementos), esta opción predecirá una lista de elementos que pueden ser de gran interés para el usuario especificado (y su selección de elementos adicional).</span><span class="sxs-lookup"><span data-stu-id="64f48-932">User to Item recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely to be of high interest for the given user (and its additional choice of items).</span></span> <span data-ttu-id="64f48-933">Las recomendaciones de U2I se basan en el historial de elementos que eran de interés para el usuario hasta el momento en que se creó el modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-933">The U2I recommendations are based on the history of items that were of interest for the user up to the time the model was built.</span></span>

<span data-ttu-id="64f48-934">Una compilación de rango es una compilación técnica que le permite aprender acerca de la utilidad de sus características.</span><span class="sxs-lookup"><span data-stu-id="64f48-934">A rank build is a technical build that allows you to learn about the usefulness of your features.</span></span> <span data-ttu-id="64f48-935">Normalmente, para obtener el mejor resultado para un modelo de recomendación que implique características, debe seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="64f48-935">Usually, in order to get the best result for a recommendation model involving features, you should take the following steps:</span></span>

* <span data-ttu-id="64f48-936">Desencadenar una compilación de rango (a menos que la puntuación de sus características sea estable) y esperar hasta que se obtenga la puntuación de la característica.</span><span class="sxs-lookup"><span data-stu-id="64f48-936">Trigger a rank build (unless the score of your features is stable) and wait till you get the feature score.</span></span>
* <span data-ttu-id="64f48-937">Recuperar el rango de las características mediante una llamada a la API [Get Features Info](#101-get-features-info-for-last-rank-build) .</span><span class="sxs-lookup"><span data-stu-id="64f48-937">Retrieve the rank of your features by calling the [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="64f48-938">Configurar una compilación de recomendación con los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="64f48-938">Configure a recommendation build with the following parameters:</span></span>
  * <span data-ttu-id="64f48-939">`useFeatureInModel` : se establece en true.</span><span class="sxs-lookup"><span data-stu-id="64f48-939">`useFeatureInModel` - Set to True.</span></span>
  * <span data-ttu-id="64f48-940">`ModelingFeatureList` : se establece en una lista de características separadas por coma con una puntuación de 2,0 o más (de acuerdo con los rangos que recuperó en el paso anterior).</span><span class="sxs-lookup"><span data-stu-id="64f48-940">`ModelingFeatureList` - Set to a comma-separated list of features with a score of 2.0 or more (according to the ranks you retrieved in the previous step).</span></span>
  * <span data-ttu-id="64f48-941">`AllowColdItemPlacement`: se establece en True.</span><span class="sxs-lookup"><span data-stu-id="64f48-941">`AllowColdItemPlacement` - Set to True.</span></span>
  * <span data-ttu-id="64f48-942">Opcionalmente, puede establecer `EnableFeatureCorrelation` en True y `ReasoningFeatureList` en la lista de características que quiere utilizar para obtener una explicación (normalmente la misma lista de características usada en el modelado o una sublista).</span><span class="sxs-lookup"><span data-stu-id="64f48-942">Optionally you can set `EnableFeatureCorrelation` to True and `ReasoningFeatureList` to the list of features you want to use for explanations (usually the same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="64f48-943">Desencadene la compilación de recomendación con los parámetros configurados.</span><span class="sxs-lookup"><span data-stu-id="64f48-943">Trigger the recommendation build with the configured parameters.</span></span>

<span data-ttu-id="64f48-944">Nota: si no configura ningún parámetro (por ejemplo, invoca la compilación de recomendación sin parámetros) o no deshabilita explícitamente el uso de características (por ejemplo, `UseFeatureInModel` se establece en False), el sistema configurará los parámetros relacionados con características para los valores explicados anteriormente en caso de que exista una compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="64f48-944">Note: If you do not configure any parameters (e.g. invoke the recommendation build without parameters) or you do not explicitly disable the usage of features (e.g. `UseFeatureInModel` set to False), the system will set up the feature-related parameters to the explained values above in case a rank build exists.</span></span>

<span data-ttu-id="64f48-945">No hay ninguna restricción sobre la ejecución de una compilación de rango y una compilación de recomendación al mismo tiempo para el mismo modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-945">There is no restriction on running a rank build and a recommendation build concurrently for the same model.</span></span> <span data-ttu-id="64f48-946">No obstante, no puede ejecutar dos compilaciones del mismo tipo en el mismo modelo en paralelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-946">Nevertheless, you cannot run two builds of the same type on the same model in parallel.</span></span>

<span data-ttu-id="64f48-947">Una compilación FBT (con frecuencia se compra junto) es otro algoritmo de recomendación denominado a veces recomendador "conservador", que resulta conveniente para catálogos que no sean de naturaleza homogénea (homogéneo: libros, películas, algunos alimentos, moda; no homogéneo: equipos y dispositivos, entre dominios, gran diversidad).</span><span class="sxs-lookup"><span data-stu-id="64f48-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="64f48-948">Nota: si los archivos de uso que ha cargado contienen el campo opcional "tipo de evento", para el modelado FBT solo se usarán eventos "Purchase".</span><span class="sxs-lookup"><span data-stu-id="64f48-948">Note: if the usage files that you uploaded contain the optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="64f48-949">Si no se proporciona ningún tipo de evento, todos los eventos se considerarán de compra.</span><span class="sxs-lookup"><span data-stu-id="64f48-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="64f48-950">11.1 Parámetros de compilación</span><span class="sxs-lookup"><span data-stu-id="64f48-950">11.1 Build parameters</span></span>
<span data-ttu-id="64f48-951">Cada tipo de compilación puede configurarse a través de un conjunto de parámetros (se muestra a continuación).</span><span class="sxs-lookup"><span data-stu-id="64f48-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="64f48-952">Si no configura los parámetros, el sistema atribuirá automáticamente valores a los parámetros según la información presente en el momento de desencadenar una compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-952">If you don't configure the parameters, the system will automatically attribute values to the parameters according to the information present at the time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="64f48-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="64f48-953">11.1.1.</span></span> <span data-ttu-id="64f48-954">Condensador de uso</span><span class="sxs-lookup"><span data-stu-id="64f48-954">Usage condenser</span></span>
<span data-ttu-id="64f48-955">Los usuarios o elementos con pocos puntos de uso podrían contener más ruido de información.</span><span class="sxs-lookup"><span data-stu-id="64f48-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="64f48-956">El sistema intenta predecir el número mínimo de puntos de uso por usuario o elemento que se usarán en un modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-956">The system attempts to predict the minimal number of usage points per user/item to be used in a model.</span></span> <span data-ttu-id="64f48-957">Este número estará dentro del intervalo definido por los parámetros ItemCutoffLowerBound y ItemCutoffUpperBound para elementos, y el intervalo definido por los parámetros UserCutOffLowerBound y UserCutoffUpperBound para usuarios.</span><span class="sxs-lookup"><span data-stu-id="64f48-957">This number will be within the range defined by the ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and the range defined by the UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="64f48-958">El efecto del condensador sobre los elementos o usuarios se puede reducir mediante el establecimiento de al menos uno de los límites correspondientes en cero.</span><span class="sxs-lookup"><span data-stu-id="64f48-958">The condenser effect on items or users can be minimized by setting at least one of the corresponding bounds to zero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="64f48-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-959">11.1.2.</span></span> <span data-ttu-id="64f48-960">Parámetros de compilación de rango</span><span class="sxs-lookup"><span data-stu-id="64f48-960">Rank build parameters</span></span>
<span data-ttu-id="64f48-961">En la tabla siguiente se describen los parámetros de compilación para una compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="64f48-961">The table below depicts the build parameters for a rank build.</span></span>

| <span data-ttu-id="64f48-962">Clave</span><span class="sxs-lookup"><span data-stu-id="64f48-962">Key</span></span> | <span data-ttu-id="64f48-963">Description</span><span class="sxs-lookup"><span data-stu-id="64f48-963">Description</span></span> | <span data-ttu-id="64f48-964">Tipo</span><span class="sxs-lookup"><span data-stu-id="64f48-964">Type</span></span> | <span data-ttu-id="64f48-965">Valor válido</span><span class="sxs-lookup"><span data-stu-id="64f48-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64f48-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="64f48-966">NumberOfModelIterations</span></span> |<span data-ttu-id="64f48-967">El número de iteraciones que realiza el modelo se refleja en el tiempo de proceso total y la precisión del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-967">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="64f48-968">Cuanto mayor sea el número, más precisión se obtendrá, pero el tiempo de proceso tardará más.</span><span class="sxs-lookup"><span data-stu-id="64f48-968">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="64f48-969">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-969">Integer</span></span> |<span data-ttu-id="64f48-970">10-50</span><span class="sxs-lookup"><span data-stu-id="64f48-970">10-50</span></span> |
| <span data-ttu-id="64f48-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="64f48-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="64f48-972">El número de dimensiones se relaciona con el número de 'características' que el modelo intentará buscar dentro de los datos.</span><span class="sxs-lookup"><span data-stu-id="64f48-972">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="64f48-973">Aumentar el número de dimensiones le permitirá ajustar mejor los resultados en clústeres más pequeños.</span><span class="sxs-lookup"><span data-stu-id="64f48-973">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="64f48-974">Sin embargo, demasiadas dimensiones impiden que el modelo encuentre correlaciones entre los elementos.</span><span class="sxs-lookup"><span data-stu-id="64f48-974">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="64f48-975">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-975">Integer</span></span> |<span data-ttu-id="64f48-976">10-40</span><span class="sxs-lookup"><span data-stu-id="64f48-976">10-40</span></span> |
| <span data-ttu-id="64f48-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="64f48-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="64f48-978">Define el límite inferior de elemento del condensador.</span><span class="sxs-lookup"><span data-stu-id="64f48-978">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="64f48-979">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f48-979">See usage condenser above.</span></span> |<span data-ttu-id="64f48-980">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-980">Integer</span></span> |<span data-ttu-id="64f48-981">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="64f48-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="64f48-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="64f48-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="64f48-983">Define el límite superior de elemento para el condensador.</span><span class="sxs-lookup"><span data-stu-id="64f48-983">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="64f48-984">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f48-984">See usage condenser above.</span></span> |<span data-ttu-id="64f48-985">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-985">Integer</span></span> |<span data-ttu-id="64f48-986">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="64f48-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="64f48-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="64f48-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="64f48-988">Define el límite inferior de usuario para el condensador.</span><span class="sxs-lookup"><span data-stu-id="64f48-988">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="64f48-989">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f48-989">See usage condenser above.</span></span> |<span data-ttu-id="64f48-990">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-990">Integer</span></span> |<span data-ttu-id="64f48-991">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="64f48-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="64f48-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="64f48-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="64f48-993">Define el límite superior de usuario para el condensador.</span><span class="sxs-lookup"><span data-stu-id="64f48-993">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="64f48-994">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f48-994">See usage condenser above.</span></span> |<span data-ttu-id="64f48-995">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-995">Integer</span></span> |<span data-ttu-id="64f48-996">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="64f48-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="64f48-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="64f48-997">11.1.3.</span></span> <span data-ttu-id="64f48-998">Parámetros de compilación de recomendación</span><span class="sxs-lookup"><span data-stu-id="64f48-998">Recommendation build parameters</span></span>
<span data-ttu-id="64f48-999">En la siguiente tabla se describen los parámetros de compilación para una compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-999">The table below depicts the build parameters for recommendation build.</span></span>

| <span data-ttu-id="64f48-1000">Clave</span><span class="sxs-lookup"><span data-stu-id="64f48-1000">Key</span></span> | <span data-ttu-id="64f48-1001">Description</span><span class="sxs-lookup"><span data-stu-id="64f48-1001">Description</span></span> | <span data-ttu-id="64f48-1002">Tipo</span><span class="sxs-lookup"><span data-stu-id="64f48-1002">Type</span></span> | <span data-ttu-id="64f48-1003">Valor válido</span><span class="sxs-lookup"><span data-stu-id="64f48-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64f48-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="64f48-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="64f48-1005">El número de iteraciones que realiza el modelo se refleja en el tiempo de proceso total y la precisión del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1005">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="64f48-1006">Cuanto mayor sea el número, más precisión se obtendrá, pero el tiempo de proceso tardará más.</span><span class="sxs-lookup"><span data-stu-id="64f48-1006">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="64f48-1007">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1007">Integer</span></span> |<span data-ttu-id="64f48-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="64f48-1008">10-50</span></span> |
| <span data-ttu-id="64f48-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="64f48-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="64f48-1010">El número de dimensiones se relaciona con el número de 'características' que el modelo intentará buscar dentro de los datos.</span><span class="sxs-lookup"><span data-stu-id="64f48-1010">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="64f48-1011">Aumentar el número de dimensiones le permitirá ajustar mejor los resultados en clústeres más pequeños.</span><span class="sxs-lookup"><span data-stu-id="64f48-1011">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="64f48-1012">Sin embargo, demasiadas dimensiones impiden que el modelo encuentre correlaciones entre los elementos.</span><span class="sxs-lookup"><span data-stu-id="64f48-1012">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="64f48-1013">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1013">Integer</span></span> |<span data-ttu-id="64f48-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="64f48-1014">10-40</span></span> |
| <span data-ttu-id="64f48-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="64f48-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="64f48-1016">Define el límite inferior de elemento del condensador.</span><span class="sxs-lookup"><span data-stu-id="64f48-1016">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="64f48-1017">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1017">See usage condenser above.</span></span> |<span data-ttu-id="64f48-1018">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1018">Integer</span></span> |<span data-ttu-id="64f48-1019">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="64f48-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="64f48-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="64f48-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="64f48-1021">Define el límite superior de elemento para el condensador.</span><span class="sxs-lookup"><span data-stu-id="64f48-1021">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="64f48-1022">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1022">See usage condenser above.</span></span> |<span data-ttu-id="64f48-1023">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1023">Integer</span></span> |<span data-ttu-id="64f48-1024">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="64f48-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="64f48-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="64f48-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="64f48-1026">Define el límite inferior de usuario para el condensador.</span><span class="sxs-lookup"><span data-stu-id="64f48-1026">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="64f48-1027">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1027">See usage condenser above.</span></span> |<span data-ttu-id="64f48-1028">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1028">Integer</span></span> |<span data-ttu-id="64f48-1029">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="64f48-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="64f48-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="64f48-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="64f48-1031">Define el límite superior de usuario para el condensador.</span><span class="sxs-lookup"><span data-stu-id="64f48-1031">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="64f48-1032">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1032">See usage condenser above.</span></span> |<span data-ttu-id="64f48-1033">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1033">Integer</span></span> |<span data-ttu-id="64f48-1034">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="64f48-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="64f48-1035">Description</span><span class="sxs-lookup"><span data-stu-id="64f48-1035">Description</span></span> |<span data-ttu-id="64f48-1036">Descripción de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1036">Build description.</span></span> |<span data-ttu-id="64f48-1037">String</span><span class="sxs-lookup"><span data-stu-id="64f48-1037">String</span></span> |<span data-ttu-id="64f48-1038">Cualquier texto, máximo 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="64f48-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="64f48-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="64f48-1039">EnableModelingInsights</span></span> |<span data-ttu-id="64f48-1040">Permite calcular métricas en el modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1040">Allows you to compute metrics on the recommendation model.</span></span> |<span data-ttu-id="64f48-1041">Booleano</span><span class="sxs-lookup"><span data-stu-id="64f48-1041">Boolean</span></span> |<span data-ttu-id="64f48-1042">True/False</span><span class="sxs-lookup"><span data-stu-id="64f48-1042">True/False</span></span> |
| <span data-ttu-id="64f48-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="64f48-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="64f48-1044">Indica si se pueden utilizar características para mejorar el modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1044">Indicates if features can be used in order to enhance the recommendation model.</span></span> |<span data-ttu-id="64f48-1045">Booleano</span><span class="sxs-lookup"><span data-stu-id="64f48-1045">Boolean</span></span> |<span data-ttu-id="64f48-1046">True/False</span><span class="sxs-lookup"><span data-stu-id="64f48-1046">True/False</span></span> |
| <span data-ttu-id="64f48-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="64f48-1047">ModelingFeatureList</span></span> |<span data-ttu-id="64f48-1048">Lista de nombres de características separados por coma que se usará en la compilación de recomendación para mejorar la recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1048">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span></span> |<span data-ttu-id="64f48-1049">String</span><span class="sxs-lookup"><span data-stu-id="64f48-1049">String</span></span> |<span data-ttu-id="64f48-1050">Nombres de características, hasta 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="64f48-1050">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="64f48-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="64f48-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="64f48-1052">Indica si la recomendación también debería insertar elementos fríos a través de la similitud de características.</span><span class="sxs-lookup"><span data-stu-id="64f48-1052">Indicates if the recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="64f48-1053">Booleano</span><span class="sxs-lookup"><span data-stu-id="64f48-1053">Boolean</span></span> |<span data-ttu-id="64f48-1054">True/False</span><span class="sxs-lookup"><span data-stu-id="64f48-1054">True/False</span></span> |
| <span data-ttu-id="64f48-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="64f48-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="64f48-1056">Indica si se pueden utilizar características en el razonamiento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="64f48-1057">Booleano</span><span class="sxs-lookup"><span data-stu-id="64f48-1057">Boolean</span></span> |<span data-ttu-id="64f48-1058">True/False</span><span class="sxs-lookup"><span data-stu-id="64f48-1058">True/False</span></span> |
| <span data-ttu-id="64f48-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="64f48-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="64f48-1060">Lista separada por comas de nombres de características que se utilizará para el razonamiento de las oraciones (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="64f48-1060">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="64f48-1061">String</span><span class="sxs-lookup"><span data-stu-id="64f48-1061">String</span></span> |<span data-ttu-id="64f48-1062">Nombres de características, hasta 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="64f48-1062">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="64f48-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="64f48-1063">EnableU2I</span></span> |<span data-ttu-id="64f48-1064">Permite la recomendación personalizada también llamada</span><span class="sxs-lookup"><span data-stu-id="64f48-1064">Allow the personalized recommendation a.k.a.</span></span> <span data-ttu-id="64f48-1065">U2I (recomendaciones de usuario a elemento).</span><span class="sxs-lookup"><span data-stu-id="64f48-1065">U2I (user to item recommendations).</span></span> |<span data-ttu-id="64f48-1066">Booleano</span><span class="sxs-lookup"><span data-stu-id="64f48-1066">Boolean</span></span> |<span data-ttu-id="64f48-1067">True/False (true de forma predeterminada)</span><span class="sxs-lookup"><span data-stu-id="64f48-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="64f48-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="64f48-1068">11.1.4.</span></span> <span data-ttu-id="64f48-1069">Parámetros de compilación FBT</span><span class="sxs-lookup"><span data-stu-id="64f48-1069">FBT build parameters</span></span>
<span data-ttu-id="64f48-1070">En la siguiente tabla se describen los parámetros de compilación para una compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1070">The table below depicts the build parameters for recommendation build.</span></span>

| <span data-ttu-id="64f48-1071">Clave</span><span class="sxs-lookup"><span data-stu-id="64f48-1071">Key</span></span> | <span data-ttu-id="64f48-1072">Description</span><span class="sxs-lookup"><span data-stu-id="64f48-1072">Description</span></span> | <span data-ttu-id="64f48-1073">Tipo</span><span class="sxs-lookup"><span data-stu-id="64f48-1073">Type</span></span> | <span data-ttu-id="64f48-1074">Valor válido (predeterminado)</span><span class="sxs-lookup"><span data-stu-id="64f48-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64f48-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="64f48-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="64f48-1076">Cómo es el modelo conservador.</span><span class="sxs-lookup"><span data-stu-id="64f48-1076">How conservative the model is.</span></span> <span data-ttu-id="64f48-1077">Número de concurrencias de elementos que deben tenerse en cuenta para el modelado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1077">Number of co-occurrences of items to be considered for modeling.</span></span> |<span data-ttu-id="64f48-1078">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1078">Integer</span></span> |<span data-ttu-id="64f48-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="64f48-1079">3-50 (6)</span></span> |
| <span data-ttu-id="64f48-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="64f48-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="64f48-1081">Limita el número de elementos en un conjunto frecuente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1081">Bounds the number of items in a frequent set.</span></span> |<span data-ttu-id="64f48-1082">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1082">Integer</span></span> |<span data-ttu-id="64f48-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="64f48-1083">2-3 (2)</span></span> |
| <span data-ttu-id="64f48-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="64f48-1084">FbtMinimalScore</span></span> |<span data-ttu-id="64f48-1085">Puntuación mínima que debe tener un conjunto frecuente para incluirlo en los resultados devueltos.</span><span class="sxs-lookup"><span data-stu-id="64f48-1085">Minimal score that a frequent set should have in order to be included in the returned results.</span></span> <span data-ttu-id="64f48-1086">Cuanto mayor sea mejor.</span><span class="sxs-lookup"><span data-stu-id="64f48-1086">The higher the better.</span></span> |<span data-ttu-id="64f48-1087">Doble</span><span class="sxs-lookup"><span data-stu-id="64f48-1087">Double</span></span> |<span data-ttu-id="64f48-1088">0 y superior (0)</span><span class="sxs-lookup"><span data-stu-id="64f48-1088">0 and above (0)</span></span> |
| <span data-ttu-id="64f48-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="64f48-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="64f48-1090">Define la función de similitud que usará la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1090">Defines the similarity function to be used by the build.</span></span> <span data-ttu-id="64f48-1091">Lift favorece la serendipia, Co-occurrence favorece la previsibilidad y Jaccard es un estupendo compromiso que comparten.</span><span class="sxs-lookup"><span data-stu-id="64f48-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between the two.</span></span> |<span data-ttu-id="64f48-1092">String</span><span class="sxs-lookup"><span data-stu-id="64f48-1092">String</span></span> |<span data-ttu-id="64f48-1093">cooccurrence, lift, jaccard (lift)</span><span class="sxs-lookup"><span data-stu-id="64f48-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="64f48-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-1094">11.2.</span></span> <span data-ttu-id="64f48-1095">Desencadenar una compilación de recomendación</span><span class="sxs-lookup"><span data-stu-id="64f48-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="64f48-1096">De forma predeterminada, esta API desencadenará una compilación de modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="64f48-1097">Para desencadenar una compilación de rango (a fin de puntuar características), debe usarse la variante de API de compilación con el parámetro de tipo de compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1097">To trigger a rank build (in order to score  features), the build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="64f48-1098">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1098">HTTP Method</span></span> | <span data-ttu-id="64f48-1099">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1100">POST</span><span class="sxs-lookup"><span data-stu-id="64f48-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1101">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="64f48-1102">ENCABEZADO</span><span class="sxs-lookup"><span data-stu-id="64f48-1102">HEADER</span></span> |<span data-ttu-id="64f48-1103">`"Content-Type", "text/xml"` (Si se envía el cuerpo de la solicitud)</span><span class="sxs-lookup"><span data-stu-id="64f48-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="64f48-1104">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1104">Parameter Name</span></span> | <span data-ttu-id="64f48-1105">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1106">modelId</span></span> |<span data-ttu-id="64f48-1107">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1107">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="64f48-1108">userDescription</span></span> |<span data-ttu-id="64f48-1109">Identificador textual del catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1109">Textual identifier of the catalog.</span></span> <span data-ttu-id="64f48-1110">Tenga en cuenta que si usa espacios debe codificarlo en su lugar con un 20 %.</span><span class="sxs-lookup"><span data-stu-id="64f48-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="64f48-1111">Vea el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="64f48-1111">See example above.</span></span><br><span data-ttu-id="64f48-1112">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="64f48-1112">Max length: 50</span></span> |
| <span data-ttu-id="64f48-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1113">apiVersion</span></span> |<span data-ttu-id="64f48-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-1115">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-1115">Request Body</span></span> |<span data-ttu-id="64f48-1116">Si se deja vacío, la compilación se ejecuta con los parámetros predeterminados.</span><span class="sxs-lookup"><span data-stu-id="64f48-1116">If left empty then the build will be executed with the default build parameters.</span></span><br><br><span data-ttu-id="64f48-1117">Si quiere establecer los parámetros de compilación, envíelos como XML en el cuerpo, como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1117">If you want to set the build parameters, send the parameters as XML into the body as in the following sample.</span></span> <span data-ttu-id="64f48-1118">(Consulte la sección "Parámetros de compilación" para obtener una explicación de los parámetros).`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="64f48-1118">(See the "Build parameters" section for an explanation of the parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="64f48-1119">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-1119">**Response**:</span></span>

<span data-ttu-id="64f48-1120">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1121">Se trata de una API asincrónica.</span><span class="sxs-lookup"><span data-stu-id="64f48-1121">This is an asynchronous API.</span></span> <span data-ttu-id="64f48-1122">Obtendrá un Id. de compilación como respuesta.</span><span class="sxs-lookup"><span data-stu-id="64f48-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="64f48-1123">Para saber cuándo ha finalizado la compilación, debe llamar a la API "Obtener estados de compilaciones de un modelo" y buscar este Id. de compilación en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="64f48-1123">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span></span> <span data-ttu-id="64f48-1124">Tenga en cuenta que una compilación puede tardar desde unos minutos hasta varias horas según el tamaño de los datos.</span><span class="sxs-lookup"><span data-stu-id="64f48-1124">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="64f48-1125">No puede usar recomendaciones hasta que no finalice la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1125">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="64f48-1126">Estado de compilación válido:</span><span class="sxs-lookup"><span data-stu-id="64f48-1126">Valid build status:</span></span>

* <span data-ttu-id="64f48-1127">Crear: se ha creado la solicitud de compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="64f48-1128">En cola: la solicitud de compilación se ha enviado y puesto en cola.</span><span class="sxs-lookup"><span data-stu-id="64f48-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="64f48-1129">Compilando: la compilación está en curso.</span><span class="sxs-lookup"><span data-stu-id="64f48-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="64f48-1130">Correcto: la compilación finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="64f48-1131">Error: la compilación finalizó con un error.</span><span class="sxs-lookup"><span data-stu-id="64f48-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="64f48-1132">Cancelada: se canceló la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="64f48-1133">Cancelando: se ha enviado una solicitud de cancelación de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1133">Cancelling - A cancel request for the build was sent.</span></span>

<span data-ttu-id="64f48-1134">Tenga en cuenta que el Id. de compilación se puede encontrar en la ruta siguiente: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="64f48-1134">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="64f48-1135">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-1135">OData XML</span></span>

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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="64f48-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="64f48-1136">11.3.</span></span> <span data-ttu-id="64f48-1137">Desencadenar compilación (recomendación, rango o FBT)</span><span class="sxs-lookup"><span data-stu-id="64f48-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="64f48-1138">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1138">HTTP Method</span></span> | <span data-ttu-id="64f48-1139">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1140">POST</span><span class="sxs-lookup"><span data-stu-id="64f48-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1141">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="64f48-1142">ENCABEZADO</span><span class="sxs-lookup"><span data-stu-id="64f48-1142">HEADER</span></span> |<span data-ttu-id="64f48-1143">`"Content-Type", "text/xml"` (Si se envía el cuerpo de la solicitud)</span><span class="sxs-lookup"><span data-stu-id="64f48-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="64f48-1144">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1144">Parameter Name</span></span> | <span data-ttu-id="64f48-1145">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1146">modelId</span></span> |<span data-ttu-id="64f48-1147">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1147">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="64f48-1148">userDescription</span></span> |<span data-ttu-id="64f48-1149">Identificador textual del catálogo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1149">Textual identifier of the catalog.</span></span> <span data-ttu-id="64f48-1150">Tenga en cuenta que si usa espacios debe codificarlo en su lugar con un 20 %.</span><span class="sxs-lookup"><span data-stu-id="64f48-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="64f48-1151">Vea el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="64f48-1151">See example above.</span></span><br><span data-ttu-id="64f48-1152">Longitud máxima: 50</span><span class="sxs-lookup"><span data-stu-id="64f48-1152">Max length: 50</span></span> |
| <span data-ttu-id="64f48-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="64f48-1153">buildType</span></span> |<span data-ttu-id="64f48-1154">Tipo de la compilación que se invocará: </span><span class="sxs-lookup"><span data-stu-id="64f48-1154">Type of the build to invoke:</span></span> <br/> <span data-ttu-id="64f48-1155">"Recomendación" para compilación de recomendación</span><span class="sxs-lookup"><span data-stu-id="64f48-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="64f48-1156">-"Categoría" para una compilación de rango</span><span class="sxs-lookup"><span data-stu-id="64f48-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="64f48-1157">- 'Fbt' para compilación FBT</span><span class="sxs-lookup"><span data-stu-id="64f48-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="64f48-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1158">apiVersion</span></span> |<span data-ttu-id="64f48-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-1160">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-1160">Request Body</span></span> |<span data-ttu-id="64f48-1161">Si se deja vacío, la compilación se ejecuta con los parámetros predeterminados.</span><span class="sxs-lookup"><span data-stu-id="64f48-1161">If left empty then the build will be executed with the default build parameters.</span></span><br><br><span data-ttu-id="64f48-1162">Si quiere establecer los parámetros de compilación, envíelos como XML en el cuerpo del mismo modo que en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1162">If you want to set build parameters, send them as XML into the body like in the following sample.</span></span> <span data-ttu-id="64f48-1163">(Consulte la sección "Parámetros de compilación" para obtener una explicación y una lista completa de los mismos).`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="64f48-1163">(See the "Build parameters" section for an explanation and full list of the parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="64f48-1164">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-1164">**Response**:</span></span>

<span data-ttu-id="64f48-1165">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1166">Se trata de una API asincrónica.</span><span class="sxs-lookup"><span data-stu-id="64f48-1166">This is an asynchronous API.</span></span> <span data-ttu-id="64f48-1167">Obtendrá un Id. de compilación como respuesta.</span><span class="sxs-lookup"><span data-stu-id="64f48-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="64f48-1168">Para saber cuándo ha finalizado la compilación, debe llamar a la API "Obtener estados de compilaciones de un modelo" y buscar este Id. de compilación en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="64f48-1168">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span></span> <span data-ttu-id="64f48-1169">Tenga en cuenta que una compilación puede tardar desde unos minutos hasta varias horas según el tamaño de los datos.</span><span class="sxs-lookup"><span data-stu-id="64f48-1169">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="64f48-1170">No puede usar recomendaciones hasta que no finalice la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1170">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="64f48-1171">Estado de compilación válido:</span><span class="sxs-lookup"><span data-stu-id="64f48-1171">Valid build status:</span></span>

* <span data-ttu-id="64f48-1172">Crear: se creó el modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1172">Create - Model was created.</span></span>
* <span data-ttu-id="64f48-1173">En cola: se desencadenó la compilación del modelo y está en la cola.</span><span class="sxs-lookup"><span data-stu-id="64f48-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="64f48-1174">Compilando: el modelo se está compilando.</span><span class="sxs-lookup"><span data-stu-id="64f48-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="64f48-1175">Correcto: la compilación finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="64f48-1176">Error: la compilación finalizó con un error.</span><span class="sxs-lookup"><span data-stu-id="64f48-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="64f48-1177">Cancelada: se canceló la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="64f48-1178">Cancelando: la compilación se está cancelando.</span><span class="sxs-lookup"><span data-stu-id="64f48-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="64f48-1179">Tenga en cuenta que el Id. de compilación se puede encontrar en la ruta siguiente: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="64f48-1179">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="64f48-1180">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-1180">OData XML</span></span>

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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="64f48-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="64f48-1181">11.4.</span></span> <span data-ttu-id="64f48-1182">Obtener el estado de compilación de un modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="64f48-1183">Recupera las compilaciones y su estado para un modelo especificado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="64f48-1184">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1184">HTTP Method</span></span> | <span data-ttu-id="64f48-1185">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1186">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1187">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1188">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1188">Parameter Name</span></span> | <span data-ttu-id="64f48-1189">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1190">modelId</span></span> |<span data-ttu-id="64f48-1191">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1191">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="64f48-1192">onlyLastBuild</span></span> |<span data-ttu-id="64f48-1193">Indica si se devolverá todo el historial de compilaciones del modelo o solo el estado de la compilación más reciente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1193">Indicates whether to return all the build history of the model or only the status of the most recent build</span></span> |
| <span data-ttu-id="64f48-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1194">apiVersion</span></span> |<span data-ttu-id="64f48-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1195">1.0</span></span> |

<span data-ttu-id="64f48-1196">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-1196">**Response**:</span></span>

<span data-ttu-id="64f48-1197">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1198">La respuesta incluye una entrada por compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1198">The response includes one entry per build.</span></span> <span data-ttu-id="64f48-1199">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-1199">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-1200">`feed/entry/content/properties/UserName` : nombre del usuario.</span><span class="sxs-lookup"><span data-stu-id="64f48-1200">`feed/entry/content/properties/UserName` - Name of the user.</span></span>
* <span data-ttu-id="64f48-1201">`feed/entry/content/properties/ModelName` : nombre del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1201">`feed/entry/content/properties/ModelName` - Name of the model.</span></span>
* <span data-ttu-id="64f48-1202">`feed/entry/content/properties/ModelId` : identificador único de modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="64f48-1203">`feed/entry/content/properties/IsDeployed`: si se implementa la compilación (también conocida como</span><span class="sxs-lookup"><span data-stu-id="64f48-1203">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="64f48-1204">compilación activa).</span><span class="sxs-lookup"><span data-stu-id="64f48-1204">active build).</span></span>
* <span data-ttu-id="64f48-1205">`feed/entry/content/properties/BuildId` : identificador único de compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="64f48-1206">`feed/entry/content/properties/BuildType` : tipo de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1206">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="64f48-1207">`feed/entry/content/properties/Status` : estado de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="64f48-1208">Puede ser uno de los siguientes: Error, Building, Queued, Cancelling, Cancelled o Success.</span><span class="sxs-lookup"><span data-stu-id="64f48-1208">Can be one of the following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="64f48-1209">`feed/entry/content/properties/StatusMessage` : mensaje de estado detallado (se aplica solo a estados concretos).</span><span class="sxs-lookup"><span data-stu-id="64f48-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="64f48-1210">`feed/entry/content/properties/Progress` : progreso de la compilación (%).</span><span class="sxs-lookup"><span data-stu-id="64f48-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="64f48-1211">`feed/entry/content/properties/StartTime` : hora de inicio de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="64f48-1212">`feed/entry/content/properties/EndTime` : hora de finalización de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="64f48-1213">`feed/entry/content/properties/ExecutionTime` : duración de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="64f48-1214">`feed/entry/content/properties/ProgressStep` : detalles sobre la fase actual de una compilación en curso.</span><span class="sxs-lookup"><span data-stu-id="64f48-1214">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span></span>

<span data-ttu-id="64f48-1215">Estado de compilación válido:</span><span class="sxs-lookup"><span data-stu-id="64f48-1215">Valid build status:</span></span>

* <span data-ttu-id="64f48-1216">Creado: se creó la entrada de solicitud de compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="64f48-1217">En cola: la solicitud de compilación se ha desencadenado y puesto en cola.</span><span class="sxs-lookup"><span data-stu-id="64f48-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="64f48-1218">Compilando: la compilación está en curso.</span><span class="sxs-lookup"><span data-stu-id="64f48-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="64f48-1219">Correcto: la compilación finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="64f48-1220">Error: la compilación finalizó con un error.</span><span class="sxs-lookup"><span data-stu-id="64f48-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="64f48-1221">Cancelada: se canceló la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="64f48-1222">Cancelando: la compilación se está cancelando.</span><span class="sxs-lookup"><span data-stu-id="64f48-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="64f48-1223">Valores válidos para el tipo de compilación:</span><span class="sxs-lookup"><span data-stu-id="64f48-1223">Valid values for build type:</span></span>

* <span data-ttu-id="64f48-1224">Rango: compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="64f48-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="64f48-1225">Recomendación: compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="64f48-1226">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-1226">OData XML</span></span>

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


### <a name="115-get-builds-status"></a><span data-ttu-id="64f48-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="64f48-1227">11.5.</span></span> <span data-ttu-id="64f48-1228">Obtener estado de compilación</span><span class="sxs-lookup"><span data-stu-id="64f48-1228">Get Builds Status</span></span>
<span data-ttu-id="64f48-1229">Recupera los estados de compilación de todos los modelos de un usuario</span><span class="sxs-lookup"><span data-stu-id="64f48-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="64f48-1230">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1230">HTTP Method</span></span> | <span data-ttu-id="64f48-1231">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1232">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1233">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1234">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1234">Parameter Name</span></span> | <span data-ttu-id="64f48-1235">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="64f48-1236">onlyLastBuild</span></span> |<span data-ttu-id="64f48-1237">Indica si se devolverá todo el historial de compilaciones del modelo o solo el estado de la compilación más reciente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1237">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="64f48-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1238">apiVersion</span></span> |<span data-ttu-id="64f48-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1239">1.0</span></span> |

<span data-ttu-id="64f48-1240">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-1240">**Response**:</span></span>

<span data-ttu-id="64f48-1241">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1242">La respuesta incluye una entrada por compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1242">The response includes one entry per build.</span></span> <span data-ttu-id="64f48-1243">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-1243">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-1244">`feed/entry/content/properties/UserName` : nombre del usuario.</span><span class="sxs-lookup"><span data-stu-id="64f48-1244">`feed/entry/content/properties/UserName` - Name of the user.</span></span>
* <span data-ttu-id="64f48-1245">`feed/entry/content/properties/ModelName` : nombre del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1245">`feed/entry/content/properties/ModelName` - Name of the model.</span></span>
* <span data-ttu-id="64f48-1246">`feed/entry/content/properties/ModelId` : identificador único de modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="64f48-1247">`feed/entry/content/properties/IsDeployed` : si se implementa la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1247">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed.</span></span>
* <span data-ttu-id="64f48-1248">`feed/entry/content/properties/BuildId` : identificador único de compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="64f48-1249">`feed/entry/content/properties/BuildType` : tipo de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1249">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="64f48-1250">`feed/entry/content/properties/Status` : estado de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="64f48-1251">Puede ser uno de los siguientes: Error, Building, Queued, Cancelled, Cancelling o Success.</span><span class="sxs-lookup"><span data-stu-id="64f48-1251">Can be one of the following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="64f48-1252">`feed/entry/content/properties/StatusMessage` : mensaje de estado detallado (se aplica solo a estados concretos).</span><span class="sxs-lookup"><span data-stu-id="64f48-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="64f48-1253">`feed/entry/content/properties/Progress` : progreso de la compilación (%).</span><span class="sxs-lookup"><span data-stu-id="64f48-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="64f48-1254">`feed/entry/content/properties/StartTime` : hora de inicio de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="64f48-1255">`feed/entry/content/properties/EndTime` : hora de finalización de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="64f48-1256">`feed/entry/content/properties/ExecutionTime` : duración de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="64f48-1257">`feed/entry/content/properties/ProgressStep` : detalles sobre la fase actual de una compilación en curso.</span><span class="sxs-lookup"><span data-stu-id="64f48-1257">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span></span>

<span data-ttu-id="64f48-1258">Estado de compilación válido:</span><span class="sxs-lookup"><span data-stu-id="64f48-1258">Valid build status:</span></span>

* <span data-ttu-id="64f48-1259">Creado: se creó la entrada de solicitud de compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="64f48-1260">En cola: la solicitud de compilación se ha desencadenado y puesto en cola.</span><span class="sxs-lookup"><span data-stu-id="64f48-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="64f48-1261">Compilando: la compilación está en curso.</span><span class="sxs-lookup"><span data-stu-id="64f48-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="64f48-1262">Correcto: la compilación finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="64f48-1263">Error: la compilación finalizó con un error.</span><span class="sxs-lookup"><span data-stu-id="64f48-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="64f48-1264">Cancelada: se canceló la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="64f48-1265">Cancelando: la compilación se está cancelando.</span><span class="sxs-lookup"><span data-stu-id="64f48-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="64f48-1266">Valores válidos para el tipo de compilación:</span><span class="sxs-lookup"><span data-stu-id="64f48-1266">Valid values for build type:</span></span>

* <span data-ttu-id="64f48-1267">Rango: compilación de rango.</span><span class="sxs-lookup"><span data-stu-id="64f48-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="64f48-1268">Recomendación: compilación de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="64f48-1269">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-1269">OData XML</span></span>

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


### <a name="116-delete-build"></a><span data-ttu-id="64f48-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="64f48-1270">11.6.</span></span> <span data-ttu-id="64f48-1271">Eliminar compilación</span><span class="sxs-lookup"><span data-stu-id="64f48-1271">Delete Build</span></span>
<span data-ttu-id="64f48-1272">Elimina una compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1272">Deletes a build.</span></span>

<span data-ttu-id="64f48-1273">NOTA: </span><span class="sxs-lookup"><span data-stu-id="64f48-1273">NOTE:</span></span> <br><span data-ttu-id="64f48-1274">no se puede eliminar una compilación activa.</span><span class="sxs-lookup"><span data-stu-id="64f48-1274">You cannot delete an active build.</span></span> <span data-ttu-id="64f48-1275">El modelo se debe actualizar a una compilación activa diferente antes de eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1275">The model should be updated to a different active build before you delete it.</span></span><br><span data-ttu-id="64f48-1276">No puede eliminar una compilación en curso.</span><span class="sxs-lookup"><span data-stu-id="64f48-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="64f48-1277">La compilación se debe cancelar primero llamando <strong>Cancelar compilación</strong>.</span><span class="sxs-lookup"><span data-stu-id="64f48-1277">You should cancel the build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="64f48-1278">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1278">HTTP Method</span></span> | <span data-ttu-id="64f48-1279">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1280">DELETE</span><span class="sxs-lookup"><span data-stu-id="64f48-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1281">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1282">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1282">Parameter Name</span></span> | <span data-ttu-id="64f48-1283">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="64f48-1284">buildId</span></span> |<span data-ttu-id="64f48-1285">Identificador único de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1285">Unique identifier of the build.</span></span> |
| <span data-ttu-id="64f48-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1286">apiVersion</span></span> |<span data-ttu-id="64f48-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1287">1.0</span></span> |

<span data-ttu-id="64f48-1288">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1288">**Response:**</span></span>

<span data-ttu-id="64f48-1289">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="64f48-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="64f48-1290">11.7.</span></span> <span data-ttu-id="64f48-1291">Cancelar compilación</span><span class="sxs-lookup"><span data-stu-id="64f48-1291">Cancel Build</span></span>
<span data-ttu-id="64f48-1292">Cancela una compilación que se encuentra en estado Building.</span><span class="sxs-lookup"><span data-stu-id="64f48-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="64f48-1293">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1293">HTTP Method</span></span> | <span data-ttu-id="64f48-1294">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="64f48-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1296">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1297">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1297">Parameter Name</span></span> | <span data-ttu-id="64f48-1298">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="64f48-1299">buildId</span></span> |<span data-ttu-id="64f48-1300">Identificador único de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1300">Unique identifier of the build.</span></span> |
| <span data-ttu-id="64f48-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1301">apiVersion</span></span> |<span data-ttu-id="64f48-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1302">1.0</span></span> |

<span data-ttu-id="64f48-1303">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1303">**Response:**</span></span>

<span data-ttu-id="64f48-1304">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="64f48-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="64f48-1305">11.8.</span></span> <span data-ttu-id="64f48-1306">Obtener parámetros de compilación</span><span class="sxs-lookup"><span data-stu-id="64f48-1306">Get Build Parameters</span></span>
<span data-ttu-id="64f48-1307">Recupera parámetros de compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="64f48-1308">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1308">HTTP Method</span></span> | <span data-ttu-id="64f48-1309">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1310">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1311">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1312">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1312">Parameter Name</span></span> | <span data-ttu-id="64f48-1313">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="64f48-1314">buildId</span></span> |<span data-ttu-id="64f48-1315">Identificador único de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1315">Unique identifier of the build.</span></span> |
| <span data-ttu-id="64f48-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1316">apiVersion</span></span> |<span data-ttu-id="64f48-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1317">1.0</span></span> |

<span data-ttu-id="64f48-1318">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1318">**Response:**</span></span>

<span data-ttu-id="64f48-1319">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1320">Esta API devuelve una colección de elementos de clave y valor.</span><span class="sxs-lookup"><span data-stu-id="64f48-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="64f48-1321">Cada elemento representa un parámetro y su valor:</span><span class="sxs-lookup"><span data-stu-id="64f48-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="64f48-1322">`feed/entry/content/properties/Key` : nombre del parámetro de compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="64f48-1323">`feed/entry/content/properties/Value` : valor del parámetro de compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="64f48-1324">En la tabla siguiente se muestra el valor que representa cada clave.</span><span class="sxs-lookup"><span data-stu-id="64f48-1324">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="64f48-1325">Clave</span><span class="sxs-lookup"><span data-stu-id="64f48-1325">Key</span></span> | <span data-ttu-id="64f48-1326">Description</span><span class="sxs-lookup"><span data-stu-id="64f48-1326">Description</span></span> | <span data-ttu-id="64f48-1327">Tipo</span><span class="sxs-lookup"><span data-stu-id="64f48-1327">Type</span></span> | <span data-ttu-id="64f48-1328">Valor válido</span><span class="sxs-lookup"><span data-stu-id="64f48-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64f48-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="64f48-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="64f48-1330">El número de iteraciones que realiza el modelo se refleja en el tiempo de proceso total y la precisión del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1330">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="64f48-1331">Cuanto mayor sea el número, más precisión se obtendrá, pero el tiempo de proceso tardará más.</span><span class="sxs-lookup"><span data-stu-id="64f48-1331">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="64f48-1332">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1332">Integer</span></span> |<span data-ttu-id="64f48-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="64f48-1333">10-50</span></span> |
| <span data-ttu-id="64f48-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="64f48-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="64f48-1335">El número de dimensiones se relaciona con el número de 'características' que el modelo intentará buscar dentro de los datos.</span><span class="sxs-lookup"><span data-stu-id="64f48-1335">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="64f48-1336">Aumentar el número de dimensiones le permitirá ajustar mejor los resultados en clústeres más pequeños.</span><span class="sxs-lookup"><span data-stu-id="64f48-1336">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="64f48-1337">Sin embargo, demasiadas dimensiones impiden que el modelo encuentre correlaciones entre los elementos.</span><span class="sxs-lookup"><span data-stu-id="64f48-1337">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="64f48-1338">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1338">Integer</span></span> |<span data-ttu-id="64f48-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="64f48-1339">10-40</span></span> |
| <span data-ttu-id="64f48-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="64f48-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="64f48-1341">Define el límite inferior de elemento del condensador.</span><span class="sxs-lookup"><span data-stu-id="64f48-1341">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="64f48-1342">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1342">See usage condenser above.</span></span> |<span data-ttu-id="64f48-1343">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1343">Integer</span></span> |<span data-ttu-id="64f48-1344">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="64f48-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="64f48-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="64f48-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="64f48-1346">Define el límite superior de elemento para el condensador.</span><span class="sxs-lookup"><span data-stu-id="64f48-1346">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="64f48-1347">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1347">See usage condenser above.</span></span> |<span data-ttu-id="64f48-1348">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1348">Integer</span></span> |<span data-ttu-id="64f48-1349">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="64f48-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="64f48-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="64f48-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="64f48-1351">Define el límite inferior de usuario para el condensador.</span><span class="sxs-lookup"><span data-stu-id="64f48-1351">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="64f48-1352">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1352">See usage condenser above.</span></span> |<span data-ttu-id="64f48-1353">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1353">Integer</span></span> |<span data-ttu-id="64f48-1354">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="64f48-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="64f48-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="64f48-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="64f48-1356">Define el límite superior de usuario para el condensador.</span><span class="sxs-lookup"><span data-stu-id="64f48-1356">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="64f48-1357">Consulte el condensador de uso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="64f48-1357">See usage condenser above.</span></span> |<span data-ttu-id="64f48-1358">Entero</span><span class="sxs-lookup"><span data-stu-id="64f48-1358">Integer</span></span> |<span data-ttu-id="64f48-1359">2 o más (0 deshabilita el condensador)</span><span class="sxs-lookup"><span data-stu-id="64f48-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="64f48-1360">Description</span><span class="sxs-lookup"><span data-stu-id="64f48-1360">Description</span></span> |<span data-ttu-id="64f48-1361">Descripción de la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1361">Build description.</span></span> |<span data-ttu-id="64f48-1362">String</span><span class="sxs-lookup"><span data-stu-id="64f48-1362">String</span></span> |<span data-ttu-id="64f48-1363">Cualquier texto, máximo 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="64f48-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="64f48-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="64f48-1364">EnableModelingInsights</span></span> |<span data-ttu-id="64f48-1365">Permite calcular métricas en el modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1365">Allows you to compute metrics on the recommendation model.</span></span> |<span data-ttu-id="64f48-1366">Booleano</span><span class="sxs-lookup"><span data-stu-id="64f48-1366">Boolean</span></span> |<span data-ttu-id="64f48-1367">True/False</span><span class="sxs-lookup"><span data-stu-id="64f48-1367">True/False</span></span> |
| <span data-ttu-id="64f48-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="64f48-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="64f48-1369">Indica si se pueden utilizar características para mejorar el modelo de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1369">Indicates if features can be used in order to enhance the recommendation model.</span></span> |<span data-ttu-id="64f48-1370">Booleano</span><span class="sxs-lookup"><span data-stu-id="64f48-1370">Boolean</span></span> |<span data-ttu-id="64f48-1371">True/False</span><span class="sxs-lookup"><span data-stu-id="64f48-1371">True/False</span></span> |
| <span data-ttu-id="64f48-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="64f48-1372">ModelingFeatureList</span></span> |<span data-ttu-id="64f48-1373">Lista de nombres de características separados por coma que se usará en la compilación de recomendación para mejorar la recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1373">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span></span> |<span data-ttu-id="64f48-1374">String</span><span class="sxs-lookup"><span data-stu-id="64f48-1374">String</span></span> |<span data-ttu-id="64f48-1375">Nombres de características, hasta 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="64f48-1375">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="64f48-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="64f48-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="64f48-1377">Indica si la recomendación también debería insertar elementos fríos a través de la similitud de características.</span><span class="sxs-lookup"><span data-stu-id="64f48-1377">Indicates if the recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="64f48-1378">Booleano</span><span class="sxs-lookup"><span data-stu-id="64f48-1378">Boolean</span></span> |<span data-ttu-id="64f48-1379">True/False</span><span class="sxs-lookup"><span data-stu-id="64f48-1379">True/False</span></span> |
| <span data-ttu-id="64f48-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="64f48-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="64f48-1381">Indica si se pueden utilizar características en el razonamiento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="64f48-1382">Booleano</span><span class="sxs-lookup"><span data-stu-id="64f48-1382">Boolean</span></span> |<span data-ttu-id="64f48-1383">True/False</span><span class="sxs-lookup"><span data-stu-id="64f48-1383">True/False</span></span> |
| <span data-ttu-id="64f48-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="64f48-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="64f48-1385">Lista separada por comas de nombres de características que se utilizará para el razonamiento de las oraciones (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="64f48-1385">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="64f48-1386">String</span><span class="sxs-lookup"><span data-stu-id="64f48-1386">String</span></span> |<span data-ttu-id="64f48-1387">Nombres de características, hasta 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="64f48-1387">Feature names, up to 512 chars</span></span> |

<span data-ttu-id="64f48-1388">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-1388">OData XML</span></span>

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

## <a name="12-recommendation"></a><span data-ttu-id="64f48-1389">12. Recomendación</span><span class="sxs-lookup"><span data-stu-id="64f48-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="64f48-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="64f48-1390">12.1.</span></span> <span data-ttu-id="64f48-1391">Obtención de recomendaciones de elemento (para la compilación activa)</span><span class="sxs-lookup"><span data-stu-id="64f48-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="64f48-1392">Obtenga recomendaciones de la compilación activa de tipo "Recommendation" o "Fbt" basadas en las lista de inicializaciones (entrada).</span><span class="sxs-lookup"><span data-stu-id="64f48-1392">Get recommendations of the active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="64f48-1393">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1393">HTTP Method</span></span> | <span data-ttu-id="64f48-1394">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1395">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1396">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1397">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1397">Parameter Name</span></span> | <span data-ttu-id="64f48-1398">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1399">modelId</span></span> |<span data-ttu-id="64f48-1400">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1400">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="64f48-1401">itemIds</span></span> |<span data-ttu-id="64f48-1402">Lista de elementos para recomendar separados por coma.</span><span class="sxs-lookup"><span data-stu-id="64f48-1402">Comma-separated list of the items to recommend for.</span></span> <br><span data-ttu-id="64f48-1403">Si la compilación activa es de tipo FBT, entonces solo puede enviar un elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1403">If the active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="64f48-1404">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="64f48-1404">Max length: 1024</span></span> |
| <span data-ttu-id="64f48-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="64f48-1405">numberOfResults</span></span> |<span data-ttu-id="64f48-1406">Número de resultados obligatorios </span><span class="sxs-lookup"><span data-stu-id="64f48-1406">Number of required results</span></span> <br> <span data-ttu-id="64f48-1407">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="64f48-1407">Max: 150</span></span> |
| <span data-ttu-id="64f48-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="64f48-1408">includeMetatadata</span></span> |<span data-ttu-id="64f48-1409">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="64f48-1409">Future use, always false</span></span> |
| <span data-ttu-id="64f48-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1410">apiVersion</span></span> |<span data-ttu-id="64f48-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1411">1.0</span></span> |

<span data-ttu-id="64f48-1412">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1412">**Response:**</span></span>

<span data-ttu-id="64f48-1413">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1414">La respuesta incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1414">The response includes one entry per recommended item.</span></span> <span data-ttu-id="64f48-1415">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-1415">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-1416">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="64f48-1417">`Feed\entry\content\properties\Name`: nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1417">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="64f48-1418">`Feed\entry\content\properties\Rating` : clasificación de la recomendación; un número alto significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="64f48-1418">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="64f48-1419">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="64f48-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="64f48-1420">En la respuesta de ejemplo a continuación se incluyen 10 elementos recomendados.</span><span class="sxs-lookup"><span data-stu-id="64f48-1420">The example response below includes 10 recommended items.</span></span>

<span data-ttu-id="64f48-1421">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-1421">OData XML</span></span>

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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="64f48-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-1422">12.2.</span></span> <span data-ttu-id="64f48-1423">Obtención de recomendaciones de elemento (de una compilación concreta)</span><span class="sxs-lookup"><span data-stu-id="64f48-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="64f48-1424">Obtiene recomendaciones de una compilación concreta de tipo "Recomendación" o "Fbt".</span><span class="sxs-lookup"><span data-stu-id="64f48-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="64f48-1425">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1425">HTTP Method</span></span> | <span data-ttu-id="64f48-1426">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1427">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1428">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1429">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1429">Parameter Name</span></span> | <span data-ttu-id="64f48-1430">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1431">modelId</span></span> |<span data-ttu-id="64f48-1432">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1432">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="64f48-1433">itemIds</span></span> |<span data-ttu-id="64f48-1434">Lista de elementos para recomendar separados por coma.</span><span class="sxs-lookup"><span data-stu-id="64f48-1434">Comma-separated list of the items to recommend for.</span></span> <br><span data-ttu-id="64f48-1435">Si la compilación activa es de tipo FBT, entonces solo puede enviar un elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1435">If the active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="64f48-1436">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="64f48-1436">Max length: 1024</span></span> |
| <span data-ttu-id="64f48-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="64f48-1437">numberOfResults</span></span> |<span data-ttu-id="64f48-1438">Número de resultados obligatorios </span><span class="sxs-lookup"><span data-stu-id="64f48-1438">Number of required results</span></span> <br> <span data-ttu-id="64f48-1439">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="64f48-1439">Max: 150</span></span> |
| <span data-ttu-id="64f48-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="64f48-1440">includeMetatadata</span></span> |<span data-ttu-id="64f48-1441">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="64f48-1441">Future use, always false</span></span> |
| <span data-ttu-id="64f48-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="64f48-1442">buildId</span></span> |<span data-ttu-id="64f48-1443">el id. de compilación que se utilizará en esta solicitud de recomendación</span><span class="sxs-lookup"><span data-stu-id="64f48-1443">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="64f48-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1444">apiVersion</span></span> |<span data-ttu-id="64f48-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1445">1.0</span></span> |

<span data-ttu-id="64f48-1446">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1446">**Response:**</span></span>

<span data-ttu-id="64f48-1447">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1448">La respuesta incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1448">The response includes one entry per recommended item.</span></span> <span data-ttu-id="64f48-1449">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-1449">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-1450">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="64f48-1451">`Feed\entry\content\properties\Name`: nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1451">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="64f48-1452">`Feed\entry\content\properties\Rating` : clasificación de la recomendación; un número alto significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="64f48-1452">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="64f48-1453">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="64f48-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="64f48-1454">Vea un ejemplo de respuesta en 12.1</span><span class="sxs-lookup"><span data-stu-id="64f48-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="64f48-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="64f48-1455">12.3.</span></span> <span data-ttu-id="64f48-1456">Obtención de recomendaciones de FBT (para la compilación activa)</span><span class="sxs-lookup"><span data-stu-id="64f48-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="64f48-1457">Obtenga recomendaciones de la compilación activa de tipo o "Fbt" basadas en las lista de inicializaciones (entrada).</span><span class="sxs-lookup"><span data-stu-id="64f48-1457">Get recommendations of the active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="64f48-1458">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1458">HTTP Method</span></span> | <span data-ttu-id="64f48-1459">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1460">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1461">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1462">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1462">Parameter Name</span></span> | <span data-ttu-id="64f48-1463">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1464">modelId</span></span> |<span data-ttu-id="64f48-1465">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1465">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="64f48-1466">itemId</span></span> |<span data-ttu-id="64f48-1467">Elemento para el que se recomienda.</span><span class="sxs-lookup"><span data-stu-id="64f48-1467">Item to recommend for.</span></span> <br><span data-ttu-id="64f48-1468">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="64f48-1468">Max length: 1024</span></span> |
| <span data-ttu-id="64f48-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="64f48-1469">numberOfResults</span></span> |<span data-ttu-id="64f48-1470">Número de resultados obligatorios </span><span class="sxs-lookup"><span data-stu-id="64f48-1470">Number of required results</span></span> <br><span data-ttu-id="64f48-1471">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="64f48-1471">Max: 150</span></span> |
| <span data-ttu-id="64f48-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="64f48-1472">minimalScore</span></span> |<span data-ttu-id="64f48-1473">Puntuación mínima que debe tener un conjunto frecuente para incluirlo en los resultados devueltos.</span><span class="sxs-lookup"><span data-stu-id="64f48-1473">Minimal score that a frequent set should have in order to be included in the returned results</span></span> |
| <span data-ttu-id="64f48-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="64f48-1474">includeMetatadata</span></span> |<span data-ttu-id="64f48-1475">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="64f48-1475">Future use, always false</span></span> |
| <span data-ttu-id="64f48-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1476">apiVersion</span></span> |<span data-ttu-id="64f48-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1477">1.0</span></span> |

<span data-ttu-id="64f48-1478">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1478">**Response:**</span></span>

<span data-ttu-id="64f48-1479">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1480">La respuesta incluye una entrada por cada elemento recomendado (un conjunto de elementos que normalmente se compran junto con el elemento de entrada/inicialización).</span><span class="sxs-lookup"><span data-stu-id="64f48-1480">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span></span> <span data-ttu-id="64f48-1481">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-1481">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-1482">`Feed\entry\content\properties\Id1`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="64f48-1483">`Feed\entry\content\properties\Name1`: nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1483">`Feed\entry\content\properties\Name1` - Name of the item.</span></span>
* <span data-ttu-id="64f48-1484">`Feed\entry\content\properties\Id2`: id. del 2º elemento recomendado (opcional).</span><span class="sxs-lookup"><span data-stu-id="64f48-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="64f48-1485">`Feed\entry\content\properties\Name2`: nombre del 2º elemento (opcional).</span><span class="sxs-lookup"><span data-stu-id="64f48-1485">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span></span>
* <span data-ttu-id="64f48-1486">`Feed\entry\content\properties\Rating` : clasificación de la recomendación; un número alto significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="64f48-1486">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="64f48-1487">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="64f48-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="64f48-1488">En la respuesta de ejemplo siguiente se incluyen 3 elementos recomendados.</span><span class="sxs-lookup"><span data-stu-id="64f48-1488">The example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="64f48-1489">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-1489">OData XML</span></span>

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

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="64f48-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="64f48-1490">12.4.</span></span> <span data-ttu-id="64f48-1491">Obtención de recomendaciones FBT (de una compilación concreta)</span><span class="sxs-lookup"><span data-stu-id="64f48-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="64f48-1492">Obtenga recomendaciones de una compilación concreta de tipo "Fbt".</span><span class="sxs-lookup"><span data-stu-id="64f48-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="64f48-1493">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1493">HTTP Method</span></span> | <span data-ttu-id="64f48-1494">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1495">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1496">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1497">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1497">Parameter Name</span></span> | <span data-ttu-id="64f48-1498">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1499">modelId</span></span> |<span data-ttu-id="64f48-1500">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1500">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="64f48-1501">itemId</span></span> |<span data-ttu-id="64f48-1502">Elemento para el que se recomienda.</span><span class="sxs-lookup"><span data-stu-id="64f48-1502">Item to recommend for.</span></span> <br><span data-ttu-id="64f48-1503">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="64f48-1503">Max length: 1024</span></span> |
| <span data-ttu-id="64f48-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="64f48-1504">numberOfResults</span></span> |<span data-ttu-id="64f48-1505">Número de resultados obligatorios </span><span class="sxs-lookup"><span data-stu-id="64f48-1505">Number of required results</span></span> <br><span data-ttu-id="64f48-1506">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="64f48-1506">Max: 150</span></span> |
| <span data-ttu-id="64f48-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="64f48-1507">minimalScore</span></span> |<span data-ttu-id="64f48-1508">Puntuación mínima que debe tener un conjunto frecuente para incluirlo en los resultados devueltos.</span><span class="sxs-lookup"><span data-stu-id="64f48-1508">Minimal score that a frequent set should have in order to be included in the returned results</span></span> |
| <span data-ttu-id="64f48-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="64f48-1509">includeMetatadata</span></span> |<span data-ttu-id="64f48-1510">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="64f48-1510">Future use, always false</span></span> |
| <span data-ttu-id="64f48-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="64f48-1511">buildId</span></span> |<span data-ttu-id="64f48-1512">el id. de compilación que se utilizará en esta solicitud de recomendación</span><span class="sxs-lookup"><span data-stu-id="64f48-1512">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="64f48-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1513">apiVersion</span></span> |<span data-ttu-id="64f48-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1514">1.0</span></span> |

<span data-ttu-id="64f48-1515">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1515">**Response:**</span></span>

<span data-ttu-id="64f48-1516">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1517">La respuesta incluye una entrada por cada elemento recomendado (un conjunto de elementos que normalmente se compran junto con el elemento de entrada/inicialización).</span><span class="sxs-lookup"><span data-stu-id="64f48-1517">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span></span> <span data-ttu-id="64f48-1518">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-1518">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-1519">`Feed\entry\content\properties\Id1`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="64f48-1520">`Feed\entry\content\properties\Name1`: nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1520">`Feed\entry\content\properties\Name1` - Name of the item.</span></span>
* <span data-ttu-id="64f48-1521">`Feed\entry\content\properties\Id2`: id. del 2º elemento recomendado (opcional).</span><span class="sxs-lookup"><span data-stu-id="64f48-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="64f48-1522">`Feed\entry\content\properties\Name2`: nombre del 2º elemento (opcional).</span><span class="sxs-lookup"><span data-stu-id="64f48-1522">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span></span>
* <span data-ttu-id="64f48-1523">`Feed\entry\content\properties\Rating` : clasificación de la recomendación; un número alto significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="64f48-1523">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="64f48-1524">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="64f48-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="64f48-1525">Vea un ejemplo de respuesta en 12.3</span><span class="sxs-lookup"><span data-stu-id="64f48-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="64f48-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="64f48-1526">12.5.</span></span> <span data-ttu-id="64f48-1527">Obtención de recomendaciones de usuario (para la compilación activa)</span><span class="sxs-lookup"><span data-stu-id="64f48-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="64f48-1528">Obtenga recomendaciones de la compilación activa de tipo "Recommendation" marcada como compilación activa.</span><span class="sxs-lookup"><span data-stu-id="64f48-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="64f48-1529">La API devolverá una lista de elementos predichos según el historial de uso del usuario.</span><span class="sxs-lookup"><span data-stu-id="64f48-1529">The API will return a list of predicted item according to the usage history of the user.</span></span>

<span data-ttu-id="64f48-1530">Notas:</span><span class="sxs-lookup"><span data-stu-id="64f48-1530">Notes:</span></span> 

1. <span data-ttu-id="64f48-1531">No hay ninguna recomendación de usuario para la generación de FBT.</span><span class="sxs-lookup"><span data-stu-id="64f48-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="64f48-1532">Si la compilación activa es FBT, este método devuelve un error.</span><span class="sxs-lookup"><span data-stu-id="64f48-1532">If the active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="64f48-1533">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1533">HTTP Method</span></span> | <span data-ttu-id="64f48-1534">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1535">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1536">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1537">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1537">Parameter Name</span></span> | <span data-ttu-id="64f48-1538">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1539">modelId</span></span> |<span data-ttu-id="64f48-1540">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1540">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-1541">userId</span><span class="sxs-lookup"><span data-stu-id="64f48-1541">userId</span></span> |<span data-ttu-id="64f48-1542">Identificador único del usuario</span><span class="sxs-lookup"><span data-stu-id="64f48-1542">Unique identifier of the user</span></span> |
| <span data-ttu-id="64f48-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="64f48-1543">numberOfResults</span></span> |<span data-ttu-id="64f48-1544">Número de resultados requeridos</span><span class="sxs-lookup"><span data-stu-id="64f48-1544">Number of required results</span></span> |
| <span data-ttu-id="64f48-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="64f48-1545">includeMetatadata</span></span> |<span data-ttu-id="64f48-1546">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="64f48-1546">Future use, always false</span></span> |
| <span data-ttu-id="64f48-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1547">apiVersion</span></span> |<span data-ttu-id="64f48-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1548">1.0</span></span> |

<span data-ttu-id="64f48-1549">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1549">**Response:**</span></span>

<span data-ttu-id="64f48-1550">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1551">La respuesta incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1551">The response includes one entry per recommended item.</span></span> <span data-ttu-id="64f48-1552">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-1552">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-1553">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="64f48-1554">`Feed\entry\content\properties\Name`: nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1554">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="64f48-1555">`Feed\entry\content\properties\Rating` : clasificación de la recomendación; un número alto significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="64f48-1555">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="64f48-1556">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="64f48-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="64f48-1557">Vea un ejemplo de respuesta en 12.1</span><span class="sxs-lookup"><span data-stu-id="64f48-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="64f48-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="64f48-1558">12.6.</span></span> <span data-ttu-id="64f48-1559">Obtención de recomendaciones de usuario con lista de elementos (para la compilación activa)</span><span class="sxs-lookup"><span data-stu-id="64f48-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="64f48-1560">Obtenga recomendaciones de la compilación activa de tipo "Recommendation" marcada como compilación activa con una lista de elementos adicional</span><span class="sxs-lookup"><span data-stu-id="64f48-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="64f48-1561">La API devolverá una lista de elementos predichos según el historial de uso del usuario y los elementos suministrados adicionales.</span><span class="sxs-lookup"><span data-stu-id="64f48-1561">The API will return a list of predicted item according to the usage history of the user and the additional provided items.</span></span>

<span data-ttu-id="64f48-1562">Notas:</span><span class="sxs-lookup"><span data-stu-id="64f48-1562">Notes:</span></span> 

1. <span data-ttu-id="64f48-1563">No hay ninguna recomendación de usuario para la generación de FBT.</span><span class="sxs-lookup"><span data-stu-id="64f48-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="64f48-1564">Si la compilación activa es FBT, este método devuelve un error.</span><span class="sxs-lookup"><span data-stu-id="64f48-1564">If the active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="64f48-1565">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1565">HTTP Method</span></span> | <span data-ttu-id="64f48-1566">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1567">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1568">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1569">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1569">Parameter Name</span></span> | <span data-ttu-id="64f48-1570">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1571">modelId</span></span> |<span data-ttu-id="64f48-1572">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1572">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-1573">userId</span><span class="sxs-lookup"><span data-stu-id="64f48-1573">userId</span></span> |<span data-ttu-id="64f48-1574">Identificador único del usuario</span><span class="sxs-lookup"><span data-stu-id="64f48-1574">Unique identifier of the user</span></span> |
| <span data-ttu-id="64f48-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="64f48-1575">itemsIds</span></span> |<span data-ttu-id="64f48-1576">Lista de elementos para recomendar separados por coma.</span><span class="sxs-lookup"><span data-stu-id="64f48-1576">Comma-separated list of the items to recommend for.</span></span> <span data-ttu-id="64f48-1577">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="64f48-1577">Max length: 1024</span></span> |
| <span data-ttu-id="64f48-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="64f48-1578">numberOfResults</span></span> |<span data-ttu-id="64f48-1579">Número de resultados requeridos</span><span class="sxs-lookup"><span data-stu-id="64f48-1579">Number of required results</span></span> |
| <span data-ttu-id="64f48-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="64f48-1580">includeMetatadata</span></span> |<span data-ttu-id="64f48-1581">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="64f48-1581">Future use, always false</span></span> |
| <span data-ttu-id="64f48-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1582">apiVersion</span></span> |<span data-ttu-id="64f48-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1583">1.0</span></span> |

<span data-ttu-id="64f48-1584">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1584">**Response:**</span></span>

<span data-ttu-id="64f48-1585">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1586">La respuesta incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1586">The response includes one entry per recommended item.</span></span> <span data-ttu-id="64f48-1587">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-1587">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-1588">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="64f48-1589">`Feed\entry\content\properties\Name`: nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1589">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="64f48-1590">`Feed\entry\content\properties\Rating` : clasificación de la recomendación; un número alto significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="64f48-1590">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="64f48-1591">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="64f48-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="64f48-1592">Vea un ejemplo de respuesta en 12.1</span><span class="sxs-lookup"><span data-stu-id="64f48-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="64f48-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="64f48-1593">12.7.</span></span> <span data-ttu-id="64f48-1594">Obtención de recomendaciones del usuario (de una compilación concreta)</span><span class="sxs-lookup"><span data-stu-id="64f48-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="64f48-1595">Obtenga recomendaciones de una compilación concreta de tipo "Recomendación" o "Fbt".</span><span class="sxs-lookup"><span data-stu-id="64f48-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="64f48-1596">La API devolverá una lista de elementos predichos según el historial de uso del usuario (usados en la compilación específica).</span><span class="sxs-lookup"><span data-stu-id="64f48-1596">The API will return a list of predicted item according to the usage history of the user (used in the specific build).</span></span>

<span data-ttu-id="64f48-1597">Nota: no hay ninguna recomendación de usuario para la generación de FBT.</span><span class="sxs-lookup"><span data-stu-id="64f48-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="64f48-1598">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1598">HTTP Method</span></span> | <span data-ttu-id="64f48-1599">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1600">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1601">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1602">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1602">Parameter Name</span></span> | <span data-ttu-id="64f48-1603">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1604">modelId</span></span> |<span data-ttu-id="64f48-1605">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1605">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-1606">userId</span><span class="sxs-lookup"><span data-stu-id="64f48-1606">userId</span></span> |<span data-ttu-id="64f48-1607">Identificador único del usuario</span><span class="sxs-lookup"><span data-stu-id="64f48-1607">Unique identifier of the user</span></span> |
| <span data-ttu-id="64f48-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="64f48-1608">numberOfResults</span></span> |<span data-ttu-id="64f48-1609">Número de resultados requeridos</span><span class="sxs-lookup"><span data-stu-id="64f48-1609">Number of required results</span></span> |
| <span data-ttu-id="64f48-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="64f48-1610">includeMetatadata</span></span> |<span data-ttu-id="64f48-1611">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="64f48-1611">Future use, always false</span></span> |
| <span data-ttu-id="64f48-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="64f48-1612">buildId</span></span> |<span data-ttu-id="64f48-1613">el id. de compilación que se utilizará en esta solicitud de recomendación</span><span class="sxs-lookup"><span data-stu-id="64f48-1613">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="64f48-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1614">apiVersion</span></span> |<span data-ttu-id="64f48-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1615">1.0</span></span> |

<span data-ttu-id="64f48-1616">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1616">**Response:**</span></span>

<span data-ttu-id="64f48-1617">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1618">La respuesta incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1618">The response includes one entry per recommended item.</span></span> <span data-ttu-id="64f48-1619">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-1619">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-1620">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="64f48-1621">`Feed\entry\content\properties\Name`: nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1621">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="64f48-1622">`Feed\entry\content\properties\Rating` : clasificación de la recomendación; un número alto significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="64f48-1622">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="64f48-1623">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="64f48-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="64f48-1624">Vea un ejemplo de respuesta en 12.1</span><span class="sxs-lookup"><span data-stu-id="64f48-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="64f48-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="64f48-1625">12.8.</span></span> <span data-ttu-id="64f48-1626">Obtención de recomendaciones de usuario con lista de elementos (de una compilación concreta)</span><span class="sxs-lookup"><span data-stu-id="64f48-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="64f48-1627">Obtenga recomendaciones de una compilación concreta de tipo "Recommendation" y la lista de elementos adicionales.</span><span class="sxs-lookup"><span data-stu-id="64f48-1627">Get user recommendations of a specific build of type "Recommendation" and the list of additional items.</span></span>

<span data-ttu-id="64f48-1628">La API devolverá una lista de elementos predichos según el historial de uso del usuario y la lista de elementos adicionales.</span><span class="sxs-lookup"><span data-stu-id="64f48-1628">The API will return a list of predicted item according to the usage history of the user and the additional list of items.</span></span>

<span data-ttu-id="64f48-1629">Nota: no hay ninguna recomendación de usuario para la generación de FBT.</span><span class="sxs-lookup"><span data-stu-id="64f48-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="64f48-1630">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1630">HTTP Method</span></span> | <span data-ttu-id="64f48-1631">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1632">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1633">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1634">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1634">Parameter Name</span></span> | <span data-ttu-id="64f48-1635">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1636">modelId</span></span> |<span data-ttu-id="64f48-1637">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1637">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-1638">userId</span><span class="sxs-lookup"><span data-stu-id="64f48-1638">userId</span></span> |<span data-ttu-id="64f48-1639">Identificador único del usuario</span><span class="sxs-lookup"><span data-stu-id="64f48-1639">Unique identifier of the user</span></span> |
| <span data-ttu-id="64f48-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="64f48-1640">itemIds</span></span> |<span data-ttu-id="64f48-1641">Lista separada por comas de los elementos para recomendar.</span><span class="sxs-lookup"><span data-stu-id="64f48-1641">Comma-separated list of the items to recommend for.</span></span> <span data-ttu-id="64f48-1642">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="64f48-1642">Max length: 1024</span></span> |
| <span data-ttu-id="64f48-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="64f48-1643">numberOfResults</span></span> |<span data-ttu-id="64f48-1644">Número de resultados requeridos</span><span class="sxs-lookup"><span data-stu-id="64f48-1644">Number of required results</span></span> |
| <span data-ttu-id="64f48-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="64f48-1645">includeMetatadata</span></span> |<span data-ttu-id="64f48-1646">Uso futuro, siempre es false</span><span class="sxs-lookup"><span data-stu-id="64f48-1646">Future use, always false</span></span> |
| <span data-ttu-id="64f48-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="64f48-1647">buildId</span></span> |<span data-ttu-id="64f48-1648">el id. de compilación que se utilizará en esta solicitud de recomendación</span><span class="sxs-lookup"><span data-stu-id="64f48-1648">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="64f48-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1649">apiVersion</span></span> |<span data-ttu-id="64f48-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1650">1.0</span></span> |

<span data-ttu-id="64f48-1651">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1651">**Response:**</span></span>

<span data-ttu-id="64f48-1652">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1653">La respuesta incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1653">The response includes one entry per recommended item.</span></span> <span data-ttu-id="64f48-1654">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-1654">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-1655">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="64f48-1656">`Feed\entry\content\properties\Name`: nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1656">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="64f48-1657">`Feed\entry\content\properties\Rating` : clasificación de la recomendación; un número alto significa mayor confianza.</span><span class="sxs-lookup"><span data-stu-id="64f48-1657">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="64f48-1658">`Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).</span><span class="sxs-lookup"><span data-stu-id="64f48-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="64f48-1659">Vea un ejemplo de respuesta en 12.1</span><span class="sxs-lookup"><span data-stu-id="64f48-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="64f48-1660">13. Historial de uso del usuario</span><span class="sxs-lookup"><span data-stu-id="64f48-1660">13. User Usage History</span></span>
<span data-ttu-id="64f48-1661">Una vez creado un modelo de recomendación, el sistema le permite recuperar el historial del usuario (los elementos asociados a un usuario específico) usado para la compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1661">Once a recommendation model was built the system will allow to retrieve the user history (items associated to a specific user) used for the build.</span></span>
<span data-ttu-id="64f48-1662">La API permite recuperar el historial del usuario</span><span class="sxs-lookup"><span data-stu-id="64f48-1662">This API allow to retrieve the user history</span></span>

<span data-ttu-id="64f48-1663">Nota: el historial del usuario actualmente solo está disponible para compilaciones de recomendación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1663">Note: the user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="64f48-1664">13.1 Recuperación del historial del usuario</span><span class="sxs-lookup"><span data-stu-id="64f48-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="64f48-1665">Recupere la lista de elementos usados en la compilación activa o en la compilación especificada para el identificador de usuario determinado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1665">Retrieve the list of item used in the active build or in the specified build for the given user id.</span></span>

| <span data-ttu-id="64f48-1666">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1666">HTTP Method</span></span> | <span data-ttu-id="64f48-1667">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1668">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1668">GET</span></span> |<span data-ttu-id="64f48-1669">Obtenga el historial de usuarios para la compilación activa.</span><span class="sxs-lookup"><span data-stu-id="64f48-1669">Get the user history for the active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="64f48-1670">Obtenga el historial de usuarios para la compilación dada `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="64f48-1670">Get the user history for the given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="64f48-1671">Ejemplo:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="64f48-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="64f48-1672">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1672">Parameter Name</span></span> | <span data-ttu-id="64f48-1673">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1674">modelId</span></span> |<span data-ttu-id="64f48-1675">identificador único del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1675">the unique identifier of the model.</span></span> |
| <span data-ttu-id="64f48-1676">userId</span><span class="sxs-lookup"><span data-stu-id="64f48-1676">userId</span></span> |<span data-ttu-id="64f48-1677">identificador único del usuario.</span><span class="sxs-lookup"><span data-stu-id="64f48-1677">the unique identifier of the user.</span></span> |
| <span data-ttu-id="64f48-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="64f48-1678">buildId</span></span> |<span data-ttu-id="64f48-1679">Parámetro opcional, permite indicar de qué compilación se debe obtener el historial del usuario</span><span class="sxs-lookup"><span data-stu-id="64f48-1679">optional parameter, allow to indicate from which build the user history should be fetch</span></span> |
| <span data-ttu-id="64f48-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1680">apiVersion</span></span> |<span data-ttu-id="64f48-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1681">1.0</span></span> |

<span data-ttu-id="64f48-1682">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1682">**Response:**</span></span>

<span data-ttu-id="64f48-1683">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1684">La respuesta incluye una entrada por cada elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1684">The response includes one entry per recommended item.</span></span> <span data-ttu-id="64f48-1685">Cada entrada tiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="64f48-1685">Each entry has the following data:</span></span>

* <span data-ttu-id="64f48-1686">`Feed\entry\content\properties\Id`: id. de elemento recomendado.</span><span class="sxs-lookup"><span data-stu-id="64f48-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="64f48-1687">`Feed\entry\content\properties\Name`: nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="64f48-1687">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="64f48-1688">`Feed\entry\content\properties\Rating` : N/D.</span><span class="sxs-lookup"><span data-stu-id="64f48-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="64f48-1689">`Feed\entry\content\properties\Reasoning` : N/D.</span><span class="sxs-lookup"><span data-stu-id="64f48-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="64f48-1690">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-1690">OData XML</span></span>

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

## <a name="14-notifications"></a><span data-ttu-id="64f48-1691">14. Notificaciones</span><span class="sxs-lookup"><span data-stu-id="64f48-1691">14. Notifications</span></span>
<span data-ttu-id="64f48-1692">Las recomendaciones de Aprendizaje automático de Azure crean notificaciones cuando se producen errores persistentes en el sistema.</span><span class="sxs-lookup"><span data-stu-id="64f48-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in the system.</span></span> <span data-ttu-id="64f48-1693">Hay 3 tipos de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="64f48-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="64f48-1694">Error de compilación: esta notificación se desencadena con cada error de compilación.</span><span class="sxs-lookup"><span data-stu-id="64f48-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="64f48-1695">Error de procesamiento de adquisición de datos: esta notificación se desencadena cuando tenemos más de 100 errores en los últimos 5 minutos en el procesamiento de eventos de uso por modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of usage events per model.</span></span>
3. <span data-ttu-id="64f48-1696">Error de consumo de recomendación: esta notificación se desencadena cuando tenemos más de 100 errores en los últimos 5 minutos en el procesamiento de solicitudes de recomendación por modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="64f48-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="64f48-1697">14.1.</span></span> <span data-ttu-id="64f48-1698">Obtener notificaciones</span><span class="sxs-lookup"><span data-stu-id="64f48-1698">Get Notifications</span></span>
<span data-ttu-id="64f48-1699">Recupera todas las notificaciones para todos los modelos o para un solo modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1699">Retrieves all the notifications for all models or for a single model.</span></span>

| <span data-ttu-id="64f48-1700">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1700">HTTP Method</span></span> | <span data-ttu-id="64f48-1701">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1702">GET</span><span class="sxs-lookup"><span data-stu-id="64f48-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1703">Obtener todas las notificaciones de todos los modelos:</span><span class="sxs-lookup"><span data-stu-id="64f48-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1704">Ejemplo de obtener las notificaciones para un modelo específico:</span><span class="sxs-lookup"><span data-stu-id="64f48-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="64f48-1705">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1705">Parameter Name</span></span> | <span data-ttu-id="64f48-1706">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1707">modelId</span></span> |<span data-ttu-id="64f48-1708">Parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="64f48-1708">Optional parameter.</span></span> <span data-ttu-id="64f48-1709">Cuando se omite, obtendrá todas las notificaciones para todos los modelos.</span><span class="sxs-lookup"><span data-stu-id="64f48-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="64f48-1710">Valor válido: identificador único del modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1710">Valid value: unique identifier of the model.</span></span> |
| <span data-ttu-id="64f48-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1711">apiVersion</span></span> |<span data-ttu-id="64f48-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-1713">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-1713">Request Body</span></span> |<span data-ttu-id="64f48-1714">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-1714">NONE</span></span> |

<span data-ttu-id="64f48-1715">**Respuesta:**</span><span class="sxs-lookup"><span data-stu-id="64f48-1715">**Response:**</span></span>

<span data-ttu-id="64f48-1716">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="64f48-1717">OData XML</span><span class="sxs-lookup"><span data-stu-id="64f48-1717">OData XML</span></span>

    The response includes one entry per notification. Each entry has the following data:
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

### <a name="142-delete-model-notifications"></a><span data-ttu-id="64f48-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="64f48-1718">14.2.</span></span> <span data-ttu-id="64f48-1719">Eliminar notificaciones de modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1719">Delete Model Notifications</span></span>
<span data-ttu-id="64f48-1720">Elimina todas las notificaciones de lectura para un modelo.</span><span class="sxs-lookup"><span data-stu-id="64f48-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="64f48-1721">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1721">HTTP Method</span></span> | <span data-ttu-id="64f48-1722">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1723">DELETE</span><span class="sxs-lookup"><span data-stu-id="64f48-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="64f48-1724">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64f48-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1725">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1725">Parameter Name</span></span> | <span data-ttu-id="64f48-1726">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="64f48-1727">modelId</span></span> |<span data-ttu-id="64f48-1728">Identificador único del modelo</span><span class="sxs-lookup"><span data-stu-id="64f48-1728">Unique identifier of the model</span></span> |
| <span data-ttu-id="64f48-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1729">apiVersion</span></span> |<span data-ttu-id="64f48-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-1731">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-1731">Request Body</span></span> |<span data-ttu-id="64f48-1732">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-1732">NONE</span></span> |

<span data-ttu-id="64f48-1733">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-1733">**Response**:</span></span>

<span data-ttu-id="64f48-1734">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="64f48-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="64f48-1735">14.3.</span></span> <span data-ttu-id="64f48-1736">Eliminar notificaciones de usuario</span><span class="sxs-lookup"><span data-stu-id="64f48-1736">Delete User Notifications</span></span>
<span data-ttu-id="64f48-1737">Elimina todas las notificaciones para todos los modelos.</span><span class="sxs-lookup"><span data-stu-id="64f48-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="64f48-1738">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="64f48-1738">HTTP Method</span></span> | <span data-ttu-id="64f48-1739">URI</span><span class="sxs-lookup"><span data-stu-id="64f48-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1740">DELETE</span><span class="sxs-lookup"><span data-stu-id="64f48-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="64f48-1741">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="64f48-1741">Parameter Name</span></span> | <span data-ttu-id="64f48-1742">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="64f48-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="64f48-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="64f48-1743">apiVersion</span></span> |<span data-ttu-id="64f48-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="64f48-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="64f48-1745">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="64f48-1745">Request Body</span></span> |<span data-ttu-id="64f48-1746">NINGUNA</span><span class="sxs-lookup"><span data-stu-id="64f48-1746">NONE</span></span> |

<span data-ttu-id="64f48-1747">**Respuesta**:</span><span class="sxs-lookup"><span data-stu-id="64f48-1747">**Response**:</span></span>

<span data-ttu-id="64f48-1748">código de estado HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="64f48-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="64f48-1749">15. Información legal</span><span class="sxs-lookup"><span data-stu-id="64f48-1749">15. Legal</span></span>
<span data-ttu-id="64f48-1750">Este documento se proporciona "como está".</span><span class="sxs-lookup"><span data-stu-id="64f48-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="64f48-1751">La información y las opiniones expresadas en este documento, como las direcciones URL y otras referencias a sitios web de Internet, pueden cambiar sin previo aviso.</span><span class="sxs-lookup"><span data-stu-id="64f48-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="64f48-1752">Algunos ejemplos mencionados se proporcionan únicamente con fines ilustrativos y son ficticios.</span><span class="sxs-lookup"><span data-stu-id="64f48-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="64f48-1753">No se pretende ninguna asociación o conexión real ni debe deducirse.</span><span class="sxs-lookup"><span data-stu-id="64f48-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="64f48-1754">Este documento no proporciona ningún derecho legal a la propiedad intelectual de ningún producto de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="64f48-1754">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="64f48-1755">Puede copiar y usar este documento con fines internos y de referencia.</span><span class="sxs-lookup"><span data-stu-id="64f48-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="64f48-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="64f48-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="64f48-1757">Todos los derechos reservados.</span><span class="sxs-lookup"><span data-stu-id="64f48-1757">All rights reserved.</span></span>

