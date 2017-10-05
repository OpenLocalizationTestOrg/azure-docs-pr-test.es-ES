---
title: Agregar operaciones a una API en Azure API Management | Microsoft Docs
description: "Obtenga información acerca de cómo agregar operaciones a una API en Administración de API de Azure."
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
ms.openlocfilehash: 105fc51c2d1152a40a5757985da47330e0b7b8cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-operations-to-an-api-in-azure-api-management"></a><span data-ttu-id="d05a0-103">Incorporación de operaciones a una API en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="d05a0-103">How to add operations to an API in Azure API Management</span></span>
<span data-ttu-id="d05a0-104">Es necesario agregar operaciones para poder utilizar una API en Administración de API.</span><span class="sxs-lookup"><span data-stu-id="d05a0-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="d05a0-105">En esta guía se muestra cómo agregar y configurar diferentes tipos de operaciones a una API en Administración de API.</span><span class="sxs-lookup"><span data-stu-id="d05a0-105">This guide shows how to add and configure different types of operations to an API in API Management.</span></span>

## <span data-ttu-id="d05a0-106"><a name="add-operation"> </a>Agregar una operación</span><span class="sxs-lookup"><span data-stu-id="d05a0-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="d05a0-107">Las operaciones se agregan y se configuran para una API en el portal del publicador.</span><span class="sxs-lookup"><span data-stu-id="d05a0-107">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="d05a0-108">Para obtener acceso al portal del publicador, haga clic en el **portal del publicador** en Azure Portal para el servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="d05a0-108">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal del publicador][api-management-management-console]

> <span data-ttu-id="d05a0-110">Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="d05a0-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="d05a0-111">Seleccione las API que desee en el portal del publicador y luego seleccione la pestaña **Operaciones** .</span><span class="sxs-lookup"><span data-stu-id="d05a0-111">Select the desired API in the publisher portal and then select the **Operations** tab.</span></span> 

![Operaciones][api-management-operations]

<span data-ttu-id="d05a0-113">Haga clic en **Agregar operación** para agregar una nueva operación.</span><span class="sxs-lookup"><span data-stu-id="d05a0-113">Click **Add Operation** to add a new operation.</span></span> <span data-ttu-id="d05a0-114">Se mostrará la ventana **Nueva operación** y la pestaña **Firma** se seleccionará de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d05a0-114">The **New operation** will be displayed and the **Signature** tab will be selected by default.</span></span>

![Agregar operación][api-management-add-operation]

<span data-ttu-id="d05a0-116">Especifique el **Verbo HTTP** seleccionándolo en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="d05a0-116">Specify the **HTTP verb** by choosing from the drop-down list.</span></span>

![HTTP method][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="d05a0-118">Defina la plantilla de URL escribiendo un fragmento de la dirección URL que conste de uno o más segmentos de ruta de la URL y de cero o más parámetros de la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="d05a0-118">Define the URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="d05a0-119">La plantilla de URL, que se anexa a la dirección URL base de la API, identifica una sola operación HTTP.</span><span class="sxs-lookup"><span data-stu-id="d05a0-119">The URL template, appended to the base URL of the API, identifies a single HTTP operation.</span></span> <span data-ttu-id="d05a0-120">Puede contener uno o más elementos de variable con nombre que se identifican mediante llaves.</span><span class="sxs-lookup"><span data-stu-id="d05a0-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="d05a0-121">Estos elementos de variable se denominan parámetros de plantilla y son valores asignados automáticamente que se extraen de la dirección URL de la solicitud al procesar la solicitud en la plataforma Administración de API.</span><span class="sxs-lookup"><span data-stu-id="d05a0-121">These variable parts are called template parameters and are dynamically assigned values extracted from the request's URL when the request is being processed by the API Management platform.</span></span>

> <span data-ttu-id="d05a0-122">La plantilla de URL puede incluir patrones de caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="d05a0-122">The URL template can include wildcard patterns.</span></span> <span data-ttu-id="d05a0-123">Por ejemplo, si se especifica `/*`, se remitirán las solicitudes para ese método HTTP al servicio final.</span><span class="sxs-lookup"><span data-stu-id="d05a0-123">For example, specifying `/*` will forward all requests for that HTTP method to the back end service.</span></span>

![URL template][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="d05a0-125">Si lo desea, especifique la **plantilla de la URL de reescritura**.</span><span class="sxs-lookup"><span data-stu-id="d05a0-125">If desired, specify the **Rewrite URL template**.</span></span> <span data-ttu-id="d05a0-126">Esto permite usar la plantilla estándar de URL para procesar solicitudes entrantes en el front-end, al tiempo que se llama al back-end mediante una URL convertida en función de la plantilla de reescritura.</span><span class="sxs-lookup"><span data-stu-id="d05a0-126">This allows you to use the standard URL template for processing incoming requests on the front-end, while calling the back-end via a converted URL according to the rewrite template.</span></span> <span data-ttu-id="d05a0-127">Deben usarse los parámetros de plantilla de la plantilla de URL en la plantilla de reescritura.</span><span class="sxs-lookup"><span data-stu-id="d05a0-127">Template parameters from the URL template should be used in the rewrite template.</span></span> <span data-ttu-id="d05a0-128">En el siguiente ejemplo se muestra cómo se puede incorporar tipo de contenido codificado en forma de segmento de ruta al servicio web del ejemplo anterior como parámetro de consulta de la API publicada mediante la plataforma Administración de API con los modelos de URL.</span><span class="sxs-lookup"><span data-stu-id="d05a0-128">The following example shows how content type encoded as path segment in the web service from the previous example can be provided as a query parameter in the API published via the API Management platform using the URL templates.</span></span>

![URL template rewrite][api-management-url-template-rewrite]

<span data-ttu-id="d05a0-130">Los usuarios que llamen a la operación usarán el formato `/customers?customerid=ALFKI`, que se asignará a `/Customers('ALFKI')` al invocar al servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="d05a0-130">Callers to the operation will use the format `/customers?customerid=ALFKI` and this will be mapped to `/Customers('ALFKI')` when the back-end service is invoked.</span></span>

<span data-ttu-id="d05a0-131">Nombre para **mostrar** y **Descripción** ofrecen una descripción de la operación y se usan para proporcionar documentación a los desarrolladores que usen esta API en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="d05a0-131">**Display** name and **Description** provide a description of the operation and are used to provide documentation to the developers using this API in the developer portal.</span></span>

![Descripción][api-management-description]

<span data-ttu-id="d05a0-133">La descripción de la operación se puede especificar como texto sin formato o HTML en el cuadro de texto **Descripción** .</span><span class="sxs-lookup"><span data-stu-id="d05a0-133">The operation description can be specified as plain text or HTML in the **Description** text box.</span></span>

## <span data-ttu-id="d05a0-134"><a name="operation-caching"> </a>Almacenamiento en caché de operaciones</span><span class="sxs-lookup"><span data-stu-id="d05a0-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="d05a0-135">El almacenamiento en caché de respuestas reduce la latencia que perciben los consumidores de la API, rebaja el consumo de ancho de banda y disminuye la carga en el servicio web HTTP que implementa la API.</span><span class="sxs-lookup"><span data-stu-id="d05a0-135">Response caching reduces latency perceived by the API consumers, lowers bandwidth consumption and decreases the load on the HTTP web service implementing the API.</span></span> 

<span data-ttu-id="d05a0-136">Para habilitar fácil y rápidamente el almacenamiento en caché de la operación, seleccione la pestaña **Caching** y active la casilla **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="d05a0-136">To easily and quickly enable caching for the operation, select the **Caching** tab and check the **Enable** checkbox.</span></span>

![Almacenamiento en caché][api-management-caching-tab]

<span data-ttu-id="d05a0-138">**Duración** especifica el período de tiempo durante el que la respuesta de la operación permanece en la caché.</span><span class="sxs-lookup"><span data-stu-id="d05a0-138">**Duration** specifies the time period during which the operation response remains in the cache.</span></span> <span data-ttu-id="d05a0-139">El valor predeterminado es 3.600 segundos o 1 hora.</span><span class="sxs-lookup"><span data-stu-id="d05a0-139">The default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="d05a0-140">Se usan claves de caché para diferenciar entre respuestas de forma que la respuesta correspondiente a cada clave de caché distinta obtenga su propio valor almacenado en caché por separado.</span><span class="sxs-lookup"><span data-stu-id="d05a0-140">Cache keys are used to differentiate between responses so that the response corresponding to each different cache key will get its own separate cached value.</span></span> <span data-ttu-id="d05a0-141">Opcionalmente, escriba los parámetros específicos de la cadena de consulta o los encabezados HTTP que se usarán para calcular los valores de clave de caché en los cuadros de texto **Variar por parámetros de cadena de consulta** y **Variar por encabezados**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="d05a0-141">Optionally, enter specific query string parameters and/or HTTP headers to be used in computing cache key values in the **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="d05a0-142">Cuando no se especifica ninguno, se usan la dirección URL de la solicitud completa y los siguientes valores de encabezado HTTP en la generación de claves de caché: **Accept** y **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="d05a0-142">When none are specified, full request URL and the following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="d05a0-143">Para obtener más información sobre el almacenamiento en caché y las directivas de almacenamiento en caché, consulte [Almacenamiento en caché de resultados de operaciones en API Management de Azure][How to cache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="d05a0-143">For more information on caching and caching policies, see [How to cache operation results in Azure API Management][How to cache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="d05a0-144"><a name="request-parameters"> </a>Parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="d05a0-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="d05a0-145">Los parámetros de la operación se administran en la pestaña Parámetros.</span><span class="sxs-lookup"><span data-stu-id="d05a0-145">Operation parameters are managed on the Parameters tab.</span></span> <span data-ttu-id="d05a0-146">Los parámetros especificados en **Modelo de URL** en la pestaña **Firma** se agregan automáticamente y solo pueden cambiarse modificando el modelo de URL.</span><span class="sxs-lookup"><span data-stu-id="d05a0-146">Parameters specified in the **URL Template** on the **Signature** tab are added automatically and can be changed only by editing the URL template.</span></span> <span data-ttu-id="d05a0-147">Se pueden introducir manualmente parámetros adicionales.</span><span class="sxs-lookup"><span data-stu-id="d05a0-147">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="d05a0-148">Para agregar un nuevo parámetro de consulta, haga clic en **Agregar parámetro de consulta** y especifique la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d05a0-148">To add a new query parameter, click **Add Query Parameter** and enter the following information:</span></span>

* <span data-ttu-id="d05a0-149">**Nombre** : nombre del parámetro.</span><span class="sxs-lookup"><span data-stu-id="d05a0-149">**Name** - parameter name.</span></span>
* <span data-ttu-id="d05a0-150">**Descripción** : breve descripción del parámetro (opcional).</span><span class="sxs-lookup"><span data-stu-id="d05a0-150">**Description** - a brief description of the parameter (optional).</span></span>
* <span data-ttu-id="d05a0-151">**Tipo** : tipo de parámetro, seleccionado en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="d05a0-151">**Type** - parameter type, selected in the drop down.</span></span>
* <span data-ttu-id="d05a0-152">**Valores** : valores que se pueden asignar a este parámetro.</span><span class="sxs-lookup"><span data-stu-id="d05a0-152">**Values** - values that can be assigned to this parameter.</span></span> <span data-ttu-id="d05a0-153">Uno de los valores se puede marcar como predeterminado (opcional).</span><span class="sxs-lookup"><span data-stu-id="d05a0-153">One of the values can be marked as default (optional).</span></span>
* <span data-ttu-id="d05a0-154">**Obligatorio** : convierte el parámetro en obligatorio al activar la casilla.</span><span class="sxs-lookup"><span data-stu-id="d05a0-154">**Required** - make the parameter mandatory by checking the checkbox.</span></span> 

![Parámetros de solicitud][api-management-request-parameters]

## <span data-ttu-id="d05a0-156"><a name="request-body"> </a>Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="d05a0-156"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="d05a0-157">Si la operación lo permite (por ejemplo, PUT, POST) y requiere un cuerpo, puede proporcionar un ejemplo del mismo en todos los formatos de representación compatibles (por ejemplo, json, XML).</span><span class="sxs-lookup"><span data-stu-id="d05a0-157">If the operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of the supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="d05a0-158">El cuerpo de la solicitud solo se usa a efectos de documentación y no se valida.</span><span class="sxs-lookup"><span data-stu-id="d05a0-158">The request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="d05a0-159">Para especificar un cuerpo de la solicitud, cambie a la pestaña **Cuerpo** .</span><span class="sxs-lookup"><span data-stu-id="d05a0-159">To enter a request body, switch to the **Body** tab.</span></span>

<span data-ttu-id="d05a0-160">Haga clic en **Agregar representación**, comience a escribir el nombre del tipo de contenido que desee (por ejemplo, aplicación/json), selecciónelo en la lista desplegable y, en el cuadro de texto, pegue el ejemplo de cuerpo de la solicitud que desee en el formato seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d05a0-160">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in the drop-down, and paste the desired request body example in the selected format into the text box.</span></span> 

![Cuerpo de la solicitud][api-management-request-body]

<span data-ttu-id="d05a0-162">Además de las representaciones, también puede especificar una descripción opcional de texto en el cuadro de texto **Descripción** .</span><span class="sxs-lookup"><span data-stu-id="d05a0-162">In additional to representations, you can also specify an optional text description in the **Description** text box.</span></span>

## <span data-ttu-id="d05a0-163"><a name="responses"> </a>Respuestas</span><span class="sxs-lookup"><span data-stu-id="d05a0-163"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="d05a0-164">Es recomendable proporcionar ejemplos de respuestas para todos los códigos de estado que puede producir la operación.</span><span class="sxs-lookup"><span data-stu-id="d05a0-164">It is a good practice to provide examples of responses for all status codes that the operation may produce.</span></span> <span data-ttu-id="d05a0-165">Cada código de estado puede tener más de un ejemplo de cuerpo de respuesta, uno para cada tipo de contenido admitido.</span><span class="sxs-lookup"><span data-stu-id="d05a0-165">Each status code may have more than one response body example, one for each of the supported content types.</span></span> 

<span data-ttu-id="d05a0-166">Para agregar una respuesta, haga clic en **Agregar** y comience a escribir el código de estado que desee.</span><span class="sxs-lookup"><span data-stu-id="d05a0-166">To add a response, click **Add** and start typing the desired status code.</span></span> <span data-ttu-id="d05a0-167">En este ejemplo, el código de estado es **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="d05a0-167">In this example the status code is **200 OK**.</span></span> <span data-ttu-id="d05a0-168">Cuando el código aparezca en la lista desplegable, selecciónelo; el código de respuesta se creará y se agregará a la operación.</span><span class="sxs-lookup"><span data-stu-id="d05a0-168">Once the code is displayed in the drop-down, select it, and the response code is created and added to your operation.</span></span>

![Response code][api-management-response-code]

<span data-ttu-id="d05a0-170">Haga clic en **Agregar representación**, comience a escribir el nombre del tipo de contenido que desee (por ejemplo, aplicación/json) y selecciónelo en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="d05a0-170">Click **Add Representation**, start typing the desired content type name (e.g. application/json) and then select it in the drop down.</span></span>

![Body content type][api-management-response-body-content-type]

<span data-ttu-id="d05a0-172">Pegue el ejemplo de cuerpo de la respuesta en el formato seleccionado en el cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="d05a0-172">Paste the response body example in the selected format into the text box.</span></span> 

![Response body][api-management-response-body]

<span data-ttu-id="d05a0-174">Si lo desea, agregue una descripción opcional en el cuadro de texto **Descripción** .</span><span class="sxs-lookup"><span data-stu-id="d05a0-174">If desired, add an optional description into the **Description** text box.</span></span>

<span data-ttu-id="d05a0-175">Una vez configurada la operación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d05a0-175">Once the operation is configured, click **Save**.</span></span>

## <span data-ttu-id="d05a0-176"><a name="next-steps"> </a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d05a0-176"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="d05a0-177">Una vez agregadas las operaciones a una API, el paso siguiente es asociar la API al producto y publicarlo para que los desarrolladores pueden llamar a las operaciones.</span><span class="sxs-lookup"><span data-stu-id="d05a0-177">Once the operations are added to an API, the next step is to associate the API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="d05a0-178">[Creación y publicación de un producto][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="d05a0-178">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md
