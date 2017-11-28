---
title: "aaaHow tooadd operations tooan API de administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd operaciones tooan API de administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a><span data-ttu-id="139e9-103">¿Cómo tooadd operaciones tooan API de administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="139e9-103">How tooadd operations tooan API in Azure API Management</span></span>
<span data-ttu-id="139e9-104">Es necesario agregar operaciones para poder utilizar una API en Administración de API.</span><span class="sxs-lookup"><span data-stu-id="139e9-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="139e9-105">Esta guía muestra cómo tooadd y configurar los distintos tipos de operaciones tooan API Administración de API.</span><span class="sxs-lookup"><span data-stu-id="139e9-105">This guide shows how tooadd and configure different types of operations tooan API in API Management.</span></span>

## <span data-ttu-id="139e9-106"><a name="add-operation"></a>Agregar una operación</span><span class="sxs-lookup"><span data-stu-id="139e9-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="139e9-107">Las operaciones se agregan y configuran tooan API en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-107">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="139e9-108">tooaccess Hola click portal, publisher **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="139e9-108">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal del publicador][api-management-management-console]

> <span data-ttu-id="139e9-110">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="139e9-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="139e9-111">Seleccione Hola deseado API en el portal para desarrolladores de hello y, a continuación, seleccione hello **Operations** ficha.</span><span class="sxs-lookup"><span data-stu-id="139e9-111">Select hello desired API in hello publisher portal and then select hello **Operations** tab.</span></span> 

![Operaciones][api-management-operations]

<span data-ttu-id="139e9-113">Haga clic en **Agregar operación** tooadd una operación de nuevo.</span><span class="sxs-lookup"><span data-stu-id="139e9-113">Click **Add Operation** tooadd a new operation.</span></span> <span data-ttu-id="139e9-114">Hola **nueva operación** se mostrarán y Hola **firma** ficha se seleccionará de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="139e9-114">hello **New operation** will be displayed and hello **Signature** tab will be selected by default.</span></span>

![Agregar operación][api-management-add-operation]

<span data-ttu-id="139e9-116">Especificar hello **verbo HTTP** mediante la elección de la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-116">Specify hello **HTTP verb** by choosing from hello drop-down list.</span></span>

![HTTP method][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="139e9-118">Definir la plantilla de dirección URL de hello escribiendo en un fragmento de dirección URL que consta de uno o más segmentos de ruta de acceso de dirección URL y cero o más parámetros de cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="139e9-118">Define hello URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="139e9-119">plantilla de dirección URL de Hello, toohello anexado de dirección URL base del programa Hola a API, identifica una única operación HTTP.</span><span class="sxs-lookup"><span data-stu-id="139e9-119">hello URL template, appended toohello base URL of hello API, identifies a single HTTP operation.</span></span> <span data-ttu-id="139e9-120">Puede contener uno o más elementos de variable con nombre que se identifican mediante llaves.</span><span class="sxs-lookup"><span data-stu-id="139e9-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="139e9-121">Estas partes variables se denominan parámetros de plantilla y se les asignan valores extraídos de dirección URL de la solicitud de hello cuando se procesa la solicitud de Hola por plataforma de administración de API de hello dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="139e9-121">These variable parts are called template parameters and are dynamically assigned values extracted from hello request's URL when hello request is being processed by hello API Management platform.</span></span>

> <span data-ttu-id="139e9-122">plantilla de dirección URL de Hello puede incluir patrones de caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="139e9-122">hello URL template can include wildcard patterns.</span></span> <span data-ttu-id="139e9-123">Por ejemplo, si se especifica `/*` al día todas las solicitudes para ese toohello del método HTTP volver finalizará servicio.</span><span class="sxs-lookup"><span data-stu-id="139e9-123">For example, specifying `/*` will forward all requests for that HTTP method toohello back end service.</span></span>

![URL template][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="139e9-125">Si lo desea, especifique hello **plantilla de dirección URL de volver a escribir**.</span><span class="sxs-lookup"><span data-stu-id="139e9-125">If desired, specify hello **Rewrite URL template**.</span></span> <span data-ttu-id="139e9-126">Esto permite plantillas estándar de dirección URL de toouse Hola para procesar las solicitudes entrantes en hello front-end, al llamar a Hola back-end a través de una dirección URL convertida según toohello vuelva a escribir plantilla.</span><span class="sxs-lookup"><span data-stu-id="139e9-126">This allows you toouse hello standard URL template for processing incoming requests on hello front-end, while calling hello back-end via a converted URL according toohello rewrite template.</span></span> <span data-ttu-id="139e9-127">Parámetros de plantilla de plantilla de dirección URL de hello deben usarse en la plantilla de reescritura de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-127">Template parameters from hello URL template should be used in hello rewrite template.</span></span> <span data-ttu-id="139e9-128">Hello en el ejemplo siguiente se muestra cómo contenido tipo codificado como segmento de ruta de acceso de servicio web de hello del anterior ejemplo de Hola puede proporcionarse como parámetro de consulta en hello API publicadas a través de hello plataforma de administración de API con plantillas de dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-128">hello following example shows how content type encoded as path segment in hello web service from hello previous example can be provided as a query parameter in hello API published via hello API Management platform using hello URL templates.</span></span>

![URL template rewrite][api-management-url-template-rewrite]

<span data-ttu-id="139e9-130">Operación de toohello de los llamadores utilizará el formato de hello `/customers?customerid=ALFKI` y se asignarán demasiado`/Customers('ALFKI')` cuando se invoca el servicio back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-130">Callers toohello operation will use hello format `/customers?customerid=ALFKI` and this will be mapped too`/Customers('ALFKI')` when hello back-end service is invoked.</span></span>

<span data-ttu-id="139e9-131">**Mostrar** nombre y **descripción** proporcionar una descripción de la operación de Hola y es utilizados tooprovide documentación toohello a los desarrolladores usar esta API en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-131">**Display** name and **Description** provide a description of hello operation and are used tooprovide documentation toohello developers using this API in hello developer portal.</span></span>

![Descripción][api-management-description]

<span data-ttu-id="139e9-133">Descripción de la operación de Hello puede especificarse como texto sin formato o HTML en hello **descripción** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="139e9-133">hello operation description can be specified as plain text or HTML in hello **Description** text box.</span></span>

## <span data-ttu-id="139e9-134"><a name="operation-caching"></a>Almacenamiento en caché de operaciones</span><span class="sxs-lookup"><span data-stu-id="139e9-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="139e9-135">Las respuestas en caché reducen la latencia percibida por los consumidores Hola API, disminuye el consumo de ancho de banda y disminuye la carga de hello en la implementación de servicio de web HTTP de Hola Hola API.</span><span class="sxs-lookup"><span data-stu-id="139e9-135">Response caching reduces latency perceived by hello API consumers, lowers bandwidth consumption and decreases hello load on hello HTTP web service implementing hello API.</span></span> 

<span data-ttu-id="139e9-136">tooeasily y habilitar rápidamente el almacenamiento en caché para la operación de hello, seleccione hello **Caching** ficha y compruebe hello **habilitar** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="139e9-136">tooeasily and quickly enable caching for hello operation, select hello **Caching** tab and check hello **Enable** checkbox.</span></span>

![Almacenamiento en caché][api-management-caching-tab]

<span data-ttu-id="139e9-138">**Duración** especifica Hola período de tiempo durante el que Hola respuesta de la operación permanece en memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-138">**Duration** specifies hello time period during which hello operation response remains in hello cache.</span></span> <span data-ttu-id="139e9-139">valor predeterminado de Hello es 3600 segundos o 1 hora.</span><span class="sxs-lookup"><span data-stu-id="139e9-139">hello default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="139e9-140">Las claves de caché son toodifferentiate utilizado entre las respuestas para que la respuesta de hello correspondiente clave de caché diferente tooeach obtendrá su propio valor almacenado en caché independiente.</span><span class="sxs-lookup"><span data-stu-id="139e9-140">Cache keys are used toodifferentiate between responses so that hello response corresponding tooeach different cache key will get its own separate cached value.</span></span> <span data-ttu-id="139e9-141">Si lo desea, especifique los parámetros de cadena de consulta específica o toobe de encabezados HTTP utilizado para calcular los valores de clave de caché en hello **variar por parámetros de cadena de consulta** y **variar por encabezados** cuadros de texto respectivamente.</span><span class="sxs-lookup"><span data-stu-id="139e9-141">Optionally, enter specific query string parameters and/or HTTP headers toobe used in computing cache key values in hello **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="139e9-142">Cuando ninguna es la dirección URL de solicitud especificado, completa y Hola después de valores de encabezado HTTP se usa en la generación de claves de caché: **Accept** y **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="139e9-142">When none are specified, full request URL and hello following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="139e9-143">Para obtener más información sobre el almacenamiento en caché y almacenamiento en caché de directivas, consulte [cómo toocache operación da como resultado en la administración de API de Azure][How toocache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="139e9-143">For more information on caching and caching policies, see [How toocache operation results in Azure API Management][How toocache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="139e9-144"><a name="request-parameters"></a>Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="139e9-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="139e9-145">Parámetros de operación se administran en la ficha parámetros de Hola. Los parámetros especificados en hello **plantilla de dirección URL** en hello **firma** ficha se agregan automáticamente y se puede cambiar mediante la edición de plantilla de dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-145">Operation parameters are managed on hello Parameters tab. Parameters specified in hello **URL Template** on hello **Signature** tab are added automatically and can be changed only by editing hello URL template.</span></span> <span data-ttu-id="139e9-146">Se pueden introducir manualmente parámetros adicionales.</span><span class="sxs-lookup"><span data-stu-id="139e9-146">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="139e9-147">tooadd un nuevo parámetro de consulta, haga clic en **Agregar parámetro de consulta** y escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="139e9-147">tooadd a new query parameter, click **Add Query Parameter** and enter hello following information:</span></span>

* <span data-ttu-id="139e9-148">**Nombre** : nombre del parámetro.</span><span class="sxs-lookup"><span data-stu-id="139e9-148">**Name** - parameter name.</span></span>
* <span data-ttu-id="139e9-149">**Descripción** -una breve descripción del parámetro hello (opcional).</span><span class="sxs-lookup"><span data-stu-id="139e9-149">**Description** - a brief description of hello parameter (optional).</span></span>
* <span data-ttu-id="139e9-150">**Tipo** -tipo de parámetro, seleccionado en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-150">**Type** - parameter type, selected in hello drop down.</span></span>
* <span data-ttu-id="139e9-151">**Valores** -valores que se pueden asignar parámetros de toothis.</span><span class="sxs-lookup"><span data-stu-id="139e9-151">**Values** - values that can be assigned toothis parameter.</span></span> <span data-ttu-id="139e9-152">Uno de los valores de hello puede marcarse como valor predeterminado (opcional).</span><span class="sxs-lookup"><span data-stu-id="139e9-152">One of hello values can be marked as default (optional).</span></span>
* <span data-ttu-id="139e9-153">**Necesario** -que parámetro hello obligatorio activando la casilla de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-153">**Required** - make hello parameter mandatory by checking hello checkbox.</span></span> 

![Parámetros de solicitud][api-management-request-parameters]

## <span data-ttu-id="139e9-155"><a name="request-body"></a>Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="139e9-155"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="139e9-156">Si permite la operación de hello (p. ej., PUT, POST) y requiere un cuerpo puede proporcionar un ejemplo del mismo en todos los de hello admite formatos de representación (por ejemplo, json, XML).</span><span class="sxs-lookup"><span data-stu-id="139e9-156">If hello operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of hello supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="139e9-157">cuerpo de la solicitud de saludo se utiliza únicamente con fines de documentación y no se valida.</span><span class="sxs-lookup"><span data-stu-id="139e9-157">hello request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="139e9-158">tooenter un cuerpo de solicitud, cambiar toohello **cuerpo** ficha.</span><span class="sxs-lookup"><span data-stu-id="139e9-158">tooenter a request body, switch toohello **Body** tab.</span></span>

<span data-ttu-id="139e9-159">Haga clic en **representación en forma de agregar**, empiece a escribir el nombre de tipo de contenido deseado (por ejemplo, application/json), selecciónelo en la lista desplegable de Hola y Hola pegar deseado ejemplo del cuerpo de solicitud con formato de hello seleccionado en el cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-159">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in hello drop-down, and paste hello desired request body example in hello selected format into hello text box.</span></span> 

![Request body][api-management-request-body]

<span data-ttu-id="139e9-161">En toorepresentations adicionales, también puede especificar una descripción de texto opcional en hello **descripción** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="139e9-161">In additional toorepresentations, you can also specify an optional text description in hello **Description** text box.</span></span>

## <span data-ttu-id="139e9-162"><a name="responses"></a>Respuestas</span><span class="sxs-lookup"><span data-stu-id="139e9-162"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="139e9-163">Es un ejemplos de tooprovide buenas prácticas de respuestas para todos los códigos de estado que se puede producir la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-163">It is a good practice tooprovide examples of responses for all status codes that hello operation may produce.</span></span> <span data-ttu-id="139e9-164">Cada código de estado puede tener más de un ejemplo de cuerpo de respuesta, uno para cada uno de hello admite tipos de contenido.</span><span class="sxs-lookup"><span data-stu-id="139e9-164">Each status code may have more than one response body example, one for each of hello supported content types.</span></span> 

<span data-ttu-id="139e9-165">tooadd una respuesta, haga clic en **agregar** y comience a escribir código de estado de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="139e9-165">tooadd a response, click **Add** and start typing hello desired status code.</span></span> <span data-ttu-id="139e9-166">En este ejemplo de estado de hello es código **200 Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="139e9-166">In this example hello status code is **200 OK**.</span></span> <span data-ttu-id="139e9-167">Una vez que se muestra el código de hello en Hola de lista desplegable, selecciónela y código de respuesta de hello es operación tooyour creado y agregado.</span><span class="sxs-lookup"><span data-stu-id="139e9-167">Once hello code is displayed in hello drop-down, select it, and hello response code is created and added tooyour operation.</span></span>

![Response code][api-management-response-code]

<span data-ttu-id="139e9-169">Haga clic en **representación en forma de agregar**, comience a escribir el nombre de tipo de contenido deseado hello (por ejemplo, application/json) y, a continuación, seleccione en Hola de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="139e9-169">Click **Add Representation**, start typing hello desired content type name (e.g. application/json) and then select it in hello drop down.</span></span>

![Body content type][api-management-response-body-content-type]

<span data-ttu-id="139e9-171">Pegar ejemplo Hola del cuerpo de respuesta en formato seleccionado de hello en el cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="139e9-171">Paste hello response body example in hello selected format into hello text box.</span></span> 

![Response body][api-management-response-body]

<span data-ttu-id="139e9-173">Si lo desea, agregue una descripción opcional en hello **descripción** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="139e9-173">If desired, add an optional description into hello **Description** text box.</span></span>

<span data-ttu-id="139e9-174">Una vez que se configura la operación de hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="139e9-174">Once hello operation is configured, click **Save**.</span></span>

## <span data-ttu-id="139e9-175"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="139e9-175"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="139e9-176">Una vez que las operaciones de Hola se agregan tooan API, Hola siguiente paso es tooassociate hello API con un producto y publicarlo para que los desarrolladores pueden llamar a sus operaciones.</span><span class="sxs-lookup"><span data-stu-id="139e9-176">Once hello operations are added tooan API, hello next step is tooassociate hello API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="139e9-177">[¿Cómo toocreate y publicación de productos][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="139e9-177">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
