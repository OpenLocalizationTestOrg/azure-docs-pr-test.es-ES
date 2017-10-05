---
title: Uso de servidores proxy en Azure Functions | Microsoft Docs
description: "Información general sobre cómo usar Azure Functions Proxies"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 102e54627a8fee721d3ed85e86a8009e706bb5b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="fd360-103">Uso de Azure Functions Proxies (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="fd360-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="fd360-104">Azure Functions Proxies actualmente se encuentra disponible en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="fd360-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="fd360-105">La versión preliminar es gratuita, pero se aplica la facturación estándar de Functions a las ejecuciones de proxy.</span><span class="sxs-lookup"><span data-stu-id="fd360-105">It is free while in preview, but standard Functions billing applies to proxy executions.</span></span> <span data-ttu-id="fd360-106">Para más información, consulte los [precios de Azure Functions](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="fd360-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="fd360-107">En este artículo se explica cómo configurar y usar Azure Functions Proxies.</span><span class="sxs-lookup"><span data-stu-id="fd360-107">This article explains how to configure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="fd360-108">Con esta característica, puede especificar puntos de conexión en su aplicación de función que se implementan con otro recurso.</span><span class="sxs-lookup"><span data-stu-id="fd360-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="fd360-109">Puede utilizar a estos servidores proxy para dividir una API grande en varias Function App (como en una arquitectura de microservicio), mientras que presenta una superficie de API única para los clientes.</span><span class="sxs-lookup"><span data-stu-id="fd360-109">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="fd360-110"><a name="enable"></a>Habilitación de Azure Functions Proxies</span><span class="sxs-lookup"><span data-stu-id="fd360-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="fd360-111">Los servidores proxy no están habilitados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fd360-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="fd360-112">Puede crear servidores proxy mientras la característica está deshabilitada, o no se ejecutarán.</span><span class="sxs-lookup"><span data-stu-id="fd360-112">You can create proxies while the feature is disabled, but they will not execute.</span></span> <span data-ttu-id="fd360-113">Para habilitar los servidores proxy, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fd360-113">To enable proxies, do the following:</span></span>

1. <span data-ttu-id="fd360-114">Abra [Azure Portal] y vaya a la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="fd360-114">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="fd360-115">Seleccione **Configuración de Function App**.</span><span class="sxs-lookup"><span data-stu-id="fd360-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="fd360-116">Cambie **Habilitar Azure Functions Proxies (versión preliminar)** a **Activado**.</span><span class="sxs-lookup"><span data-stu-id="fd360-116">Switch **Enable Azure Functions Proxies (preview)** to **On**.</span></span>

<span data-ttu-id="fd360-117">También puede volver aquí para actualizar el tiempo de ejecución del proxy a medida que haya nuevas características disponibles.</span><span class="sxs-lookup"><span data-stu-id="fd360-117">You can also return here to update the proxy runtime as new features become available.</span></span>


## <span data-ttu-id="fd360-118"><a name="create"></a>Creación de un proxy</span><span class="sxs-lookup"><span data-stu-id="fd360-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="fd360-119">En esta sección se explica cómo crear un proxy en el portal de Functions.</span><span class="sxs-lookup"><span data-stu-id="fd360-119">This section shows you how to create a proxy in the Functions portal.</span></span>

1. <span data-ttu-id="fd360-120">Abra [Azure Portal] y vaya a la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="fd360-120">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="fd360-121">En el panel izquierdo, seleccione **Nuevo servidor proxy**.</span><span class="sxs-lookup"><span data-stu-id="fd360-121">In the left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="fd360-122">Proporcione un nombre para el proxy.</span><span class="sxs-lookup"><span data-stu-id="fd360-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="fd360-123">Configure el punto de conexión expuesto en esta aplicación de función; para ello, especifique la **plantilla de ruta** y los **métodos HTTP**.</span><span class="sxs-lookup"><span data-stu-id="fd360-123">Configure the endpoint that's exposed on this function app by specifying the **route template** and **HTTP methods**.</span></span> <span data-ttu-id="fd360-124">Estos parámetros se comportan según las reglas de los [desencadenadores HTTP].</span><span class="sxs-lookup"><span data-stu-id="fd360-124">These parameters behave according to the rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="fd360-125">Establezca la **dirección URL de back-end** en otro punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="fd360-125">Set the **backend URL** to another endpoint.</span></span> <span data-ttu-id="fd360-126">El punto de conexión podría tratarse de una función en otra aplicación de función o podría ser cualquier otra API.</span><span class="sxs-lookup"><span data-stu-id="fd360-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="fd360-127">El valor no necesita ser estático y puede hacer referencia a la [configuración de la aplicación] y a [parámetros de la solicitud de cliente original].</span><span class="sxs-lookup"><span data-stu-id="fd360-127">The value does not need to be static, and it can reference [application settings] and [parameters from the original client request].</span></span>
6. <span data-ttu-id="fd360-128">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fd360-128">Click **Create**.</span></span>

<span data-ttu-id="fd360-129">El proxy ahora existe como un nuevo punto de conexión en la Function App.</span><span class="sxs-lookup"><span data-stu-id="fd360-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="fd360-130">Desde una perspectiva de cliente, es equivalente a un HttpTrigger en Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="fd360-130">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="fd360-131">Puede probar el nuevo proxy; para ello, copie la dirección URL del proxy y pruébela con el cliente HTTP favorito.</span><span class="sxs-lookup"><span data-stu-id="fd360-131">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="fd360-132"><a name="modify-requests-responses"></a>Modificación de solicitudes y respuestas</span><span class="sxs-lookup"><span data-stu-id="fd360-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="fd360-133">Con Azure Functions Proxies, puede modificar solicitudes y respuestas desde el back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-133">With Azure Functions Proxies, you can modify requests to and responses from the back end.</span></span> <span data-ttu-id="fd360-134">Estas transformaciones pueden usar variables, como se define en [Uso de variables].</span><span class="sxs-lookup"><span data-stu-id="fd360-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="fd360-135"><a name="modify-backend-request"></a>Modificación de la solicitud de back-end</span><span class="sxs-lookup"><span data-stu-id="fd360-135"><a name="modify-backend-request"></a>Modify the back-end request</span></span>

<span data-ttu-id="fd360-136">De forma predeterminada, la solicitud de back-end se inicializa como copia de la solicitud original.</span><span class="sxs-lookup"><span data-stu-id="fd360-136">By default, the back-end request is initialized as a copy of the original request.</span></span> <span data-ttu-id="fd360-137">Además de establecer la dirección URL de back-end, se pueden realizar cambios en el método HTTP, los encabezados y los parámetros de cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="fd360-137">In addition to setting the back-end URL, you can make changes to the HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="fd360-138">Los valores modificados pueden hacer referencia a la [configuración de la aplicación] y a los [parámetros de la solicitud de cliente original].</span><span class="sxs-lookup"><span data-stu-id="fd360-138">The modified values can reference [application settings] and [parameters from the original client request].</span></span>

<span data-ttu-id="fd360-139">Actualmente, no existe ninguna experiencia de portal para modificar las solicitudes de back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="fd360-140">Para aprender a aplicar esta funcionalidad desde proxies.json, consulte [Definición de un objeto requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="fd360-140">To learn how to apply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="fd360-141"><a name="modify-response"></a>Modificación de la respuesta</span><span class="sxs-lookup"><span data-stu-id="fd360-141"><a name="modify-response"></a>Modify the response</span></span>

<span data-ttu-id="fd360-142">De forma predeterminada, la respuesta del cliente se inicializa como copia de la respuesta de back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-142">By default, the client response is initialized as a copy of the back-end response.</span></span> <span data-ttu-id="fd360-143">Puede realizar cambios en el código de estado, la expresión del motivo, los encabezados y el cuerpo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="fd360-143">You can make changes to the response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="fd360-144">Los valores modificados pueden hacer referencia a la [configuración de la aplicación], a [parámetros de la solicitud de cliente original] y a [parámetros de la respuesta de back-end].</span><span class="sxs-lookup"><span data-stu-id="fd360-144">The modified values can reference [application settings], [parameters from the original client request], and [parameters from the back-end response].</span></span>

<span data-ttu-id="fd360-145">Actualmente, no existe ninguna experiencia de portal para modificar respuestas.</span><span class="sxs-lookup"><span data-stu-id="fd360-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="fd360-146">Para aprender a aplicar esta funcionalidad desde proxies.json, consulte [Definición de un objeto responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="fd360-146">To learn how to apply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="fd360-147"><a name="using-variables"></a>Uso de variables</span><span class="sxs-lookup"><span data-stu-id="fd360-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="fd360-148">La configuración de un proxy no necesita ser estática.</span><span class="sxs-lookup"><span data-stu-id="fd360-148">The configuration for a proxy does not need to be static.</span></span> <span data-ttu-id="fd360-149">Puede condicionarlo para que use variables de la solicitud original, la respuesta de back-end o la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd360-149">You can condition it to use variables from the original request, the back-end response, or application settings.</span></span>

### <span data-ttu-id="fd360-150"><a name="request-parameters"></a>Referencia a los parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="fd360-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="fd360-151">Puede usar parámetros de solicitud como entradas para la propiedad de dirección URL de back-end o como parte de la modificación de solicitudes y respuestas.</span><span class="sxs-lookup"><span data-stu-id="fd360-151">You can use request parameters as inputs to the back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="fd360-152">Algunos parámetros pueden enlazarse desde la plantilla de ruta especificada en la configuración de proxy base, y otros pueden proceder de propiedades de la solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="fd360-152">Some parameters can be bound from the route template that's specified in the base proxy configuration, and others can come from properties of the incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="fd360-153">Parámetros de plantilla de ruta</span><span class="sxs-lookup"><span data-stu-id="fd360-153">Route template parameters</span></span>
<span data-ttu-id="fd360-154">Los parámetros que se usan en la plantilla de ruta están disponibles para hacer referencia a ellos por su nombre.</span><span class="sxs-lookup"><span data-stu-id="fd360-154">Parameters that are used in the route template are available to be referenced by name.</span></span> <span data-ttu-id="fd360-155">Los nombres de parámetro van rodeados de llaves ({}).</span><span class="sxs-lookup"><span data-stu-id="fd360-155">The parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="fd360-156">Por ejemplo, si un proxy tiene una plantilla de ruta, como `/pets/{petId}`, la dirección URL de back-end puede incluir el valor de `{petId}`, como en `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="fd360-156">For example, if a proxy has a route template, such as `/pets/{petId}`, the back-end URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="fd360-157">Si la plantilla de ruta finaliza en un carácter comodín, como `/api/{*restOfPath}`, el valor `{restOfPath}` es una representación de cadena de los segmentos de ruta de acceso restantes procedentes de la solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="fd360-157">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` is a string representation of the remaining path segments from the incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="fd360-158">Parámetros de solicitud adicionales</span><span class="sxs-lookup"><span data-stu-id="fd360-158">Additional request parameters</span></span>
<span data-ttu-id="fd360-159">Además de los parámetros de la plantilla de ruta, pueden usarse los siguientes valores en la configuración:</span><span class="sxs-lookup"><span data-stu-id="fd360-159">In addition to the route template parameters, the following values can be used in config values:</span></span>

* <span data-ttu-id="fd360-160">**{request.method}**: método HTTP que se usa en la solicitud original.</span><span class="sxs-lookup"><span data-stu-id="fd360-160">**{request.method}**: The HTTP method that's used on the original request.</span></span>
* <span data-ttu-id="fd360-161">**{request.headers.\<nombreDeEncabezado\>}**: encabezado que puede leerse desde la solicitud original.</span><span class="sxs-lookup"><span data-stu-id="fd360-161">**{request.headers.\<HeaderName\>}**: A header that can be read from the original request.</span></span> <span data-ttu-id="fd360-162">Reemplace *\<nombreDeEncabezado\>* por el nombre del encabezado que desea leer.</span><span class="sxs-lookup"><span data-stu-id="fd360-162">Replace *\<HeaderName\>* with the name of the header that you want to read.</span></span> <span data-ttu-id="fd360-163">Si el encabezado no se incluye en la solicitud, el valor será una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="fd360-163">If the header is not included on the request, the value will be the empty string.</span></span>
* <span data-ttu-id="fd360-164">**{request.querystring.\<nombreDeParámetro\>}**: parámetro de cadena de consulta que se puede leer desde la solicitud original.</span><span class="sxs-lookup"><span data-stu-id="fd360-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from the original request.</span></span> <span data-ttu-id="fd360-165">Reemplace *\<nombreDeParámetro\>* por el nombre del parámetro que desea leer.</span><span class="sxs-lookup"><span data-stu-id="fd360-165">Replace *\<ParameterName\>* with the name of the parameter that you want to read.</span></span> <span data-ttu-id="fd360-166">Si el parámetro no se incluye en la solicitud, el valor será una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="fd360-166">If the parameter is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="fd360-167"><a name="response-parameters"></a>Referencia a parámetros de respuesta de back-end</span><span class="sxs-lookup"><span data-stu-id="fd360-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="fd360-168">Los parámetros de respuesta pueden utilizarse como parte de la modificación de la respuesta al cliente.</span><span class="sxs-lookup"><span data-stu-id="fd360-168">Response parameters can be used as part of modifying the response to the client.</span></span> <span data-ttu-id="fd360-169">Se pueden usar los siguientes valores en la configuración:</span><span class="sxs-lookup"><span data-stu-id="fd360-169">The following values can be used in config values:</span></span>

* <span data-ttu-id="fd360-170">**{backend.response.statusCode}**: código de estado HTTP que se devuelve en la respuesta de back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-170">**{backend.response.statusCode}**: The HTTP status code that's returned on the back-end response.</span></span>
* <span data-ttu-id="fd360-171">**{backend.response.statusReason}**: la frase de motivo HTTP que se devuelve en la respuesta de back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-171">**{backend.response.statusReason}**: The HTTP reason phrase that's returned on the back-end response.</span></span>
* <span data-ttu-id="fd360-172">**{backend.response.headers.\<nombreDeEncabezado\>}**: encabezado que puede leerse desde la respuesta de back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from the back-end response.</span></span> <span data-ttu-id="fd360-173">Reemplace *\<nombreDeEncabezado\>* por el nombre del encabezado que desea leer.</span><span class="sxs-lookup"><span data-stu-id="fd360-173">Replace *\<HeaderName\>* with the name of the header you want to read.</span></span> <span data-ttu-id="fd360-174">Si el encabezado no se incluye en la solicitud, el valor será una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="fd360-174">If the header is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="fd360-175"><a name="use-appsettings"></a>Referencia a la configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="fd360-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="fd360-176">También puede hacer referencia a la [configuración de la aplicación definida para la aplicación de función](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) rodeando el nombre de la configuración con signos de porcentaje (%).</span><span class="sxs-lookup"><span data-stu-id="fd360-176">You can also reference [application settings defined for the function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs (%).</span></span>

<span data-ttu-id="fd360-177">Por ejemplo, en una dirección URL de back-end *https://%ORDER_PROCESSING_HOST%/api/orders*, "%ORDER_PROCESSING_HOST%" se reemplaza por el valor de la configuración de ORDER_PROCESSING_HOST.</span><span class="sxs-lookup"><span data-stu-id="fd360-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="fd360-178">Use la configuración de la aplicación para hosts back-end si tiene varias implementaciones o entornos de prueba.</span><span class="sxs-lookup"><span data-stu-id="fd360-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="fd360-179">De este modo, puede asegurarse de que siempre se comunica con el back-end correcto para ese entorno.</span><span class="sxs-lookup"><span data-stu-id="fd360-179">That way, you can make sure that you are always talking to the right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="fd360-180">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="fd360-180">Advanced configuration</span></span>

<span data-ttu-id="fd360-181">Los servidores proxy que configure se almacenan en un archivo proxies.json, ubicado en la raíz de un directorio de la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="fd360-181">The proxies that you configure are stored in a proxies.json file, which is located in the root of a function app directory.</span></span> <span data-ttu-id="fd360-182">Puede editar este archivo manualmente e implementarlo como parte de la aplicación cuando se utiliza cualquiera de los [métodos de implementación](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) compatibles con Functions.</span><span class="sxs-lookup"><span data-stu-id="fd360-182">You can manually edit this file and deploy it as part of your app when you use any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="fd360-183">La característica debe estar [habilitada](#enable) para poder procesar el archivo.</span><span class="sxs-lookup"><span data-stu-id="fd360-183">The feature must be [enabled](#enable) for the file to be processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="fd360-184">Si no ha configurado alguno de los métodos de implementación, también puede trabajar con el archivo proxies.json en el portal.</span><span class="sxs-lookup"><span data-stu-id="fd360-184">If you have not set up one of the deployment methods, you can also work with the proxies.json file in the portal.</span></span> <span data-ttu-id="fd360-185">Vaya a la aplicación de función y seleccione **Características de la plataforma** y **Editor de App Service**.</span><span class="sxs-lookup"><span data-stu-id="fd360-185">Go to your function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="fd360-186">Al hacerlo, puede ver toda la estructura de archivos de la aplicación de función y realizar cambios.</span><span class="sxs-lookup"><span data-stu-id="fd360-186">By doing so, you can view the entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="fd360-187">El archivo proxies.json lo define un objeto de servidores proxy, compuesto de servidores proxy con nombre y de sus definiciones.</span><span class="sxs-lookup"><span data-stu-id="fd360-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="fd360-188">De forma opcional, si el editor lo admite, puede hacer referencia a un [esquema JSON](http://json.schemastore.org/proxies) para completar el código.</span><span class="sxs-lookup"><span data-stu-id="fd360-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="fd360-189">Un archivo de ejemplo puede tener el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="fd360-189">An example file might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

<span data-ttu-id="fd360-190">Cada proxy tiene un nombre descriptivo, como *proxy1* en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="fd360-190">Each proxy has a friendly name, such as *proxy1* in the preceding example.</span></span> <span data-ttu-id="fd360-191">El objeto de definición de proxy correspondiente se define mediante las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="fd360-191">The corresponding proxy definition object is defined by the following properties:</span></span>

* <span data-ttu-id="fd360-192">**matchCondition**: (requerida) un objeto que define las solicitudes que desencadenan la ejecución de este proxy.</span><span class="sxs-lookup"><span data-stu-id="fd360-192">**matchCondition**: Required--an object defining the requests that trigger the execution of this proxy.</span></span> <span data-ttu-id="fd360-193">Contiene dos propiedades compartidas con los [desencadenadores HTTP]:</span><span class="sxs-lookup"><span data-stu-id="fd360-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="fd360-194">_methods_: una matriz de los métodos HTTP a los que responde el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="fd360-194">_methods_: An array of the HTTP methods that the proxy responds to.</span></span> <span data-ttu-id="fd360-195">Si no se especifica, el proxy responde a todos los métodos HTTP de la ruta.</span><span class="sxs-lookup"><span data-stu-id="fd360-195">If it is not specified, the proxy responds to all HTTP methods on the route.</span></span>
    * <span data-ttu-id="fd360-196">_route_: (requerida) define la plantilla de ruta y controla a qué direcciones URL de solicitud responde el proxy.</span><span class="sxs-lookup"><span data-stu-id="fd360-196">_route_: Required--defines the route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="fd360-197">A diferencia de los desencadenadores HTTP, no hay ningún valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="fd360-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="fd360-198">**backendUri**: la dirección URL del recurso de back-end a la que se redirigirá la solicitud mediante proxy.</span><span class="sxs-lookup"><span data-stu-id="fd360-198">**backendUri**: The URL of the back-end resource to which the request should be proxied.</span></span> <span data-ttu-id="fd360-199">Este valor puede hacer referencia a la configuración de la aplicación y a parámetros de la solicitud de cliente original.</span><span class="sxs-lookup"><span data-stu-id="fd360-199">This value can reference application settings and parameters from the original client request.</span></span> <span data-ttu-id="fd360-200">Si no se incluye esta propiedad, Azure Functions responde con el mensaje HTTP 200 - Correcto.</span><span class="sxs-lookup"><span data-stu-id="fd360-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="fd360-201">**requestOverrides**: objeto que define transformaciones a la solicitud de back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-201">**requestOverrides**: An object that defines transformations to the back-end request.</span></span> <span data-ttu-id="fd360-202">Consulte [Definición de un objeto requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="fd360-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="fd360-203">**responseOverrides**: objeto que define transformaciones a la respuesta del cliente.</span><span class="sxs-lookup"><span data-stu-id="fd360-203">**responseOverrides**: An object that defines transformations to the client response.</span></span> <span data-ttu-id="fd360-204">Consulte [Definición de un objeto responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="fd360-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="fd360-205">La propiedad de ruta de Azure Functions Proxies no respeta la propiedad routePrefix de la configuración del host de Functions.</span><span class="sxs-lookup"><span data-stu-id="fd360-205">The route property Azure Functions Proxies does not honor the routePrefix property of the Functions host configuration.</span></span> <span data-ttu-id="fd360-206">Si desea incluir un prefijo como /api, se debe incluir en la propiedad de ruta.</span><span class="sxs-lookup"><span data-stu-id="fd360-206">If you want to include a prefix such as /api, it must be included in the route property.</span></span>

### <span data-ttu-id="fd360-207"><a name="requestOverrides"></a>Definición de un objeto requestOverrides</span><span class="sxs-lookup"><span data-stu-id="fd360-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="fd360-208">El objeto requestOverrides define los cambios realizados en la solicitud cuando se llama al recurso de back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-208">The requestOverrides object defines changes made to the request when the back-end resource is called.</span></span> <span data-ttu-id="fd360-209">El objeto se define mediante las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="fd360-209">The object is defined by the following properties:</span></span>

* <span data-ttu-id="fd360-210">**backend.request.method**: método HTTP que se usa para llamar al back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-210">**backend.request.method**: The HTTP method that's used to call the back end.</span></span>
* <span data-ttu-id="fd360-211">**backend.request.querystring.\<nombreDeParámetro\>**: parámetro de cadena de consulta que se puede establecer para llamar al back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for the call to the back end.</span></span> <span data-ttu-id="fd360-212">Reemplace *\<nombreDeParámetro\>* por el nombre del parámetro que desea establecer.</span><span class="sxs-lookup"><span data-stu-id="fd360-212">Replace *\<ParameterName\>* with the name of the parameter that you want to set.</span></span> <span data-ttu-id="fd360-213">Si se proporciona una cadena vacía, el parámetro no se incluye en la solicitud de back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-213">If the empty string is provided, the parameter is not included on the back-end request.</span></span>
* <span data-ttu-id="fd360-214">**backend.request.headers.\<nombreDeEncabezado\>**: encabezado que se puede establecer para llamar al back end.</span><span class="sxs-lookup"><span data-stu-id="fd360-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for the call to the back end.</span></span> <span data-ttu-id="fd360-215">Reemplace *\<nombreDeEncabezado\>* por el nombre del encabezado que desea establecer.</span><span class="sxs-lookup"><span data-stu-id="fd360-215">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="fd360-216">Si se proporciona una cadena vacía, el encabezado no se incluye en la solicitud de back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-216">If you provide the empty string, the header is not included on the back-end request.</span></span>

<span data-ttu-id="fd360-217">Los valores pueden hacer referencia a la configuración de la aplicación y a los parámetros de la solicitud de cliente original.</span><span class="sxs-lookup"><span data-stu-id="fd360-217">Values can reference application settings and parameters from the original client request.</span></span>

<span data-ttu-id="fd360-218">Una configuración de ejemplo puede tener el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="fd360-218">An example configuration might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <span data-ttu-id="fd360-219"><a name="responseOverrides"></a>Definición de un objeto responseOverrides</span><span class="sxs-lookup"><span data-stu-id="fd360-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="fd360-220">El objeto requestOverrides define los cambios realizados en la respuesta que se pasa de nuevo al cliente.</span><span class="sxs-lookup"><span data-stu-id="fd360-220">The requestOverrides object defines changes that are made to the response that's passed back to the client.</span></span> <span data-ttu-id="fd360-221">El objeto se define mediante las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="fd360-221">The object is defined by the following properties:</span></span>

* <span data-ttu-id="fd360-222">**response.statusCode**: código de estado HTTP que se va a devolver al cliente.</span><span class="sxs-lookup"><span data-stu-id="fd360-222">**response.statusCode**: The HTTP status code to be returned to the client.</span></span>
* <span data-ttu-id="fd360-223">**response.statusReason**: frase de motivo HTTP que se va a devolver al cliente.</span><span class="sxs-lookup"><span data-stu-id="fd360-223">**response.statusReason**: The HTTP reason phrase to be returned to the client.</span></span>
* <span data-ttu-id="fd360-224">**response.body**: representación de cadena del cuerpo que se va a devolver al cliente.</span><span class="sxs-lookup"><span data-stu-id="fd360-224">**response.body**: The string representation of the body to be returned to the client.</span></span>
* <span data-ttu-id="fd360-225">**response.headers.\<nombreDeEncabezado\>**: encabezado que se puede establecer para la respuesta al cliente.</span><span class="sxs-lookup"><span data-stu-id="fd360-225">**response.headers.\<HeaderName\>**: A header that can be set for the response to the client.</span></span> <span data-ttu-id="fd360-226">Reemplace *\<nombreDeEncabezado\>* por el nombre del encabezado que desea establecer.</span><span class="sxs-lookup"><span data-stu-id="fd360-226">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="fd360-227">Si se proporciona una cadena vacía, el encabezado no se incluye en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="fd360-227">If you provide the empty string, the header is not included on the response.</span></span>

<span data-ttu-id="fd360-228">Los valores pueden hacer referencia a la configuración de la aplicación, a parámetros de la solicitud de cliente original y a parámetros de la respuesta de back-end.</span><span class="sxs-lookup"><span data-stu-id="fd360-228">Values can reference application settings, parameters from the original client request, and parameters from the back-end response.</span></span>

<span data-ttu-id="fd360-229">Una configuración de ejemplo puede tener el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="fd360-229">An example configuration might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> <span data-ttu-id="fd360-230">En este ejemplo, el cuerpo se define directamente, por lo que no se necesita la propiedad `backendUri`.</span><span class="sxs-lookup"><span data-stu-id="fd360-230">In this example, the body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="fd360-231">En el ejemplo, se muestra cómo usar Azure Functions Proxies para simular las API.</span><span class="sxs-lookup"><span data-stu-id="fd360-231">The example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

<span data-ttu-id="fd360-232">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="fd360-232">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="fd360-233">[desencadenadores HTTP]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span><span class="sxs-lookup"><span data-stu-id="fd360-233">[HTTP triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span></span>
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
<span data-ttu-id="fd360-234">[Definición de un objeto requestOverrides]: #requestOverrides</span><span class="sxs-lookup"><span data-stu-id="fd360-234">[Define a requestOverrides object]: #requestOverrides</span></span>
<span data-ttu-id="fd360-235">[Definición de un objeto responseOverrides]: #responseOverrides</span><span class="sxs-lookup"><span data-stu-id="fd360-235">[Define a responseOverrides object]: #responseOverrides</span></span>
<span data-ttu-id="fd360-236">[configuración de la aplicación]: #use-appsettings</span><span class="sxs-lookup"><span data-stu-id="fd360-236">[application settings]: #use-appsettings</span></span>
<span data-ttu-id="fd360-237">[Uso de variables]: #using-variables</span><span class="sxs-lookup"><span data-stu-id="fd360-237">[Use variables]: #using-variables</span></span>
<span data-ttu-id="fd360-238">[parámetros de la solicitud de cliente original]: #request-parameters</span><span class="sxs-lookup"><span data-stu-id="fd360-238">[parameters from the original client request]: #request-parameters</span></span>
<span data-ttu-id="fd360-239">[parámetros de la respuesta de back-end]: #response-parameters</span><span class="sxs-lookup"><span data-stu-id="fd360-239">[parameters from the back-end response]: #response-parameters</span></span>
