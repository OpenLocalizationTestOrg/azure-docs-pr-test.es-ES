---
title: aaaWork con servidores proxy en las funciones de Azure | Documentos de Microsoft
description: "Información general sobre cómo toouse servidores proxy de las funciones de Azure"
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
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="3dd27-103">Uso de Azure Functions Proxies (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="3dd27-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="3dd27-104">Azure Functions Proxies actualmente se encuentra disponible en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="3dd27-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="3dd27-105">Es gratuito, mientras que en la vista previa, pero las funciones estándar facturación aplica tooproxy ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="3dd27-105">It is free while in preview, but standard Functions billing applies tooproxy executions.</span></span> <span data-ttu-id="3dd27-106">Para más información, consulte los [precios de Azure Functions](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="3dd27-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="3dd27-107">Este artículo se explica cómo tooconfigure y trabajar con servidores proxy de las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd27-107">This article explains how tooconfigure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="3dd27-108">Con esta característica, puede especificar puntos de conexión en su aplicación de función que se implementan con otro recurso.</span><span class="sxs-lookup"><span data-stu-id="3dd27-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="3dd27-109">Puede utilizar estos servidores proxy toobreak una API grande en varias aplicaciones de función (como en una arquitectura de microservicio), mientras que presenta una superficie de API única para los clientes.</span><span class="sxs-lookup"><span data-stu-id="3dd27-109">You can use these proxies toobreak a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="3dd27-110"><a name="enable"></a>Habilitación de Azure Functions Proxies</span><span class="sxs-lookup"><span data-stu-id="3dd27-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="3dd27-111">Los servidores proxy no están habilitados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3dd27-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="3dd27-112">Puede crear a servidores proxy mientras Hola característica está deshabilitada, pero no ejecutará.</span><span class="sxs-lookup"><span data-stu-id="3dd27-112">You can create proxies while hello feature is disabled, but they will not execute.</span></span> <span data-ttu-id="3dd27-113">servidores proxy tooenable, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="3dd27-113">tooenable proxies, do hello following:</span></span>

1. <span data-ttu-id="3dd27-114">Abra hello [portal de Azure], y, a continuación, vaya tooyour función aplicación.</span><span class="sxs-lookup"><span data-stu-id="3dd27-114">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="3dd27-115">Seleccione **Configuración de Function App**.</span><span class="sxs-lookup"><span data-stu-id="3dd27-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="3dd27-116">Conmutador **Habilitar proxy de funciones de Azure (vista previa)** demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="3dd27-116">Switch **Enable Azure Functions Proxies (preview)** too**On**.</span></span>

<span data-ttu-id="3dd27-117">También puede devolver aquí en tiempo de ejecución de tooupdate Hola proxy nuevas características estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="3dd27-117">You can also return here tooupdate hello proxy runtime as new features become available.</span></span>


## <span data-ttu-id="3dd27-118"><a name="create"></a>Creación de un proxy</span><span class="sxs-lookup"><span data-stu-id="3dd27-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="3dd27-119">Esta sección muestra cómo toocreate un proxy en Hola portal de funciones.</span><span class="sxs-lookup"><span data-stu-id="3dd27-119">This section shows you how toocreate a proxy in hello Functions portal.</span></span>

1. <span data-ttu-id="3dd27-120">Abra hello [portal de Azure], y, a continuación, vaya tooyour función aplicación.</span><span class="sxs-lookup"><span data-stu-id="3dd27-120">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="3dd27-121">En el panel izquierdo de hello, seleccione **nuevo proxy**.</span><span class="sxs-lookup"><span data-stu-id="3dd27-121">In hello left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="3dd27-122">Proporcione un nombre para el proxy.</span><span class="sxs-lookup"><span data-stu-id="3dd27-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="3dd27-123">Configurar el punto de conexión de Hola que se expone en esta aplicación de función mediante la especificación de hello **plantilla de ruta** y **métodos HTTP**.</span><span class="sxs-lookup"><span data-stu-id="3dd27-123">Configure hello endpoint that's exposed on this function app by specifying hello **route template** and **HTTP methods**.</span></span> <span data-ttu-id="3dd27-124">Estos parámetros comportan correspondiente reglas toohello para [HTTP desencadenadores].</span><span class="sxs-lookup"><span data-stu-id="3dd27-124">These parameters behave according toohello rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="3dd27-125">Conjunto hello **dirección URL de back-end** tooanother punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="3dd27-125">Set hello **backend URL** tooanother endpoint.</span></span> <span data-ttu-id="3dd27-126">El punto de conexión podría tratarse de una función en otra aplicación de función o podría ser cualquier otra API.</span><span class="sxs-lookup"><span data-stu-id="3dd27-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="3dd27-127">Hello valor no necesita toobe estático, y puede hacer referencia a [configuración de la aplicación] y [parámetros de solicitud de cliente original hello].</span><span class="sxs-lookup"><span data-stu-id="3dd27-127">hello value does not need toobe static, and it can reference [application settings] and [parameters from hello original client request].</span></span>
6. <span data-ttu-id="3dd27-128">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3dd27-128">Click **Create**.</span></span>

<span data-ttu-id="3dd27-129">El proxy ahora existe como un nuevo punto de conexión en la Function App.</span><span class="sxs-lookup"><span data-stu-id="3dd27-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="3dd27-130">Desde una perspectiva de cliente, es equivalente tooan HttpTrigger en las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd27-130">From a client perspective, it is equivalent tooan HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="3dd27-131">Puede probar el nuevo proxy copiando Hola dirección URL del Proxy y probarlo con el cliente HTTP favorito.</span><span class="sxs-lookup"><span data-stu-id="3dd27-131">You can try out your new proxy by copying hello Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="3dd27-132"><a name="modify-requests-responses"></a>Modificación de solicitudes y respuestas</span><span class="sxs-lookup"><span data-stu-id="3dd27-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="3dd27-133">Con servidores proxy de las funciones de Azure, puede modificar las respuestas de tooand de las solicitudes de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-133">With Azure Functions Proxies, you can modify requests tooand responses from hello back end.</span></span> <span data-ttu-id="3dd27-134">Estas transformaciones pueden usar variables, como se define en [Uso de variables].</span><span class="sxs-lookup"><span data-stu-id="3dd27-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="3dd27-135"><a name="modify-backend-request"></a>Modificar la solicitud de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="3dd27-135"><a name="modify-backend-request"></a>Modify hello back-end request</span></span>

<span data-ttu-id="3dd27-136">De forma predeterminada, solicitud de back-end de Hola se inicializa como una copia de la solicitud original Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-136">By default, hello back-end request is initialized as a copy of hello original request.</span></span> <span data-ttu-id="3dd27-137">Además toosetting Hola back-end URL, puede hacer cambios toohello HTTP método, encabezados y parámetros de cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="3dd27-137">In addition toosetting hello back-end URL, you can make changes toohello HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="3dd27-138">Hello los valores modificados pueden hacer referencia a [configuración de la aplicación] y [parámetros de solicitud de cliente original hello].</span><span class="sxs-lookup"><span data-stu-id="3dd27-138">hello modified values can reference [application settings] and [parameters from hello original client request].</span></span>

<span data-ttu-id="3dd27-139">Actualmente, no existe ninguna experiencia de portal para modificar las solicitudes de back-end.</span><span class="sxs-lookup"><span data-stu-id="3dd27-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="3dd27-140">toolearn tooapply esta capacidad a proxies.json, vea [definir un objeto requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="3dd27-140">toolearn how tooapply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="3dd27-141"><a name="modify-response"></a>Modificar respuesta Hola</span><span class="sxs-lookup"><span data-stu-id="3dd27-141"><a name="modify-response"></a>Modify hello response</span></span>

<span data-ttu-id="3dd27-142">De forma predeterminada, se inicializa respuesta del cliente hello como una copia de la respuesta de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-142">By default, hello client response is initialized as a copy of hello back-end response.</span></span> <span data-ttu-id="3dd27-143">Puede realizar el código de estado de la respuesta de toohello de cambios, motivo, encabezados y cuerpo.</span><span class="sxs-lookup"><span data-stu-id="3dd27-143">You can make changes toohello response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="3dd27-144">Hello los valores modificados pueden hacer referencia a [configuración de la aplicación], [parámetros de solicitud de cliente original hello], y [parámetros de respuesta de back-end de hello].</span><span class="sxs-lookup"><span data-stu-id="3dd27-144">hello modified values can reference [application settings], [parameters from hello original client request], and [parameters from hello back-end response].</span></span>

<span data-ttu-id="3dd27-145">Actualmente, no existe ninguna experiencia de portal para modificar respuestas.</span><span class="sxs-lookup"><span data-stu-id="3dd27-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="3dd27-146">toolearn tooapply esta capacidad a proxies.json, vea [definir un objeto responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="3dd27-146">toolearn how tooapply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="3dd27-147"><a name="using-variables"></a>Uso de variables</span><span class="sxs-lookup"><span data-stu-id="3dd27-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="3dd27-148">configuración de Hola para un servidor proxy no es necesario toobe estático.</span><span class="sxs-lookup"><span data-stu-id="3dd27-148">hello configuration for a proxy does not need toobe static.</span></span> <span data-ttu-id="3dd27-149">Puede condición toouse variables de solicitud original hello, respuesta de back-end de Hola o configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3dd27-149">You can condition it toouse variables from hello original request, hello back-end response, or application settings.</span></span>

### <span data-ttu-id="3dd27-150"><a name="request-parameters"></a>Referencia a los parámetros de solicitud</span><span class="sxs-lookup"><span data-stu-id="3dd27-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="3dd27-151">Puede usar los parámetros de solicitud, las entradas de la propiedad de dirección URL de back-end de toohello o como parte de la modificación de las solicitudes y respuestas.</span><span class="sxs-lookup"><span data-stu-id="3dd27-151">You can use request parameters as inputs toohello back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="3dd27-152">Pueden enlazar algunos parámetros de plantilla de ruta de Hola que se especifica en la configuración de proxy base hello y otros usuarios pueden proceder de propiedades de solicitud entrante de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-152">Some parameters can be bound from hello route template that's specified in hello base proxy configuration, and others can come from properties of hello incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="3dd27-153">Parámetros de plantilla de ruta</span><span class="sxs-lookup"><span data-stu-id="3dd27-153">Route template parameters</span></span>
<span data-ttu-id="3dd27-154">Parámetros que se usan en la plantilla de ruta de hello son toobe disponible al que hace referencia por su nombre.</span><span class="sxs-lookup"><span data-stu-id="3dd27-154">Parameters that are used in hello route template are available toobe referenced by name.</span></span> <span data-ttu-id="3dd27-155">los nombres de parámetro Hello están entre llaves ({}).</span><span class="sxs-lookup"><span data-stu-id="3dd27-155">hello parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="3dd27-156">Por ejemplo, si un proxy tiene una plantilla de ruta, como `/pets/{petId}`, dirección URL de back-end de hello puede incluir el valor de Hola de `{petId}`, como en `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="3dd27-156">For example, if a proxy has a route template, such as `/pets/{petId}`, hello back-end URL can include hello value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="3dd27-157">Si plantilla de ruta de hello finaliza en un carácter comodín, como `/api/{*restOfPath}`, Hola valor `{restOfPath}` es una representación de cadena de hello restantes segmentos de ruta de acceso de solicitud entrante de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-157">If hello route template terminates in a wildcard, such as `/api/{*restOfPath}`, hello value `{restOfPath}` is a string representation of hello remaining path segments from hello incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="3dd27-158">Parámetros de solicitud adicionales</span><span class="sxs-lookup"><span data-stu-id="3dd27-158">Additional request parameters</span></span>
<span data-ttu-id="3dd27-159">Además toohello enrutar parámetros de plantilla, Hola después de valores se puede utilizar en valores de configuración:</span><span class="sxs-lookup"><span data-stu-id="3dd27-159">In addition toohello route template parameters, hello following values can be used in config values:</span></span>

* <span data-ttu-id="3dd27-160">**{request.method}** : Hola método HTTP que se usa en la solicitud original Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-160">**{request.method}**: hello HTTP method that's used on hello original request.</span></span>
* <span data-ttu-id="3dd27-161">**{request.headers. \<HeaderName\>}**: un encabezado que se puede leer desde la solicitud original Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-161">**{request.headers.\<HeaderName\>}**: A header that can be read from hello original request.</span></span> <span data-ttu-id="3dd27-162">Reemplace  *\<HeaderName\>*  con nombre hello del encabezado de Hola que desea tooread.</span><span class="sxs-lookup"><span data-stu-id="3dd27-162">Replace *\<HeaderName\>* with hello name of hello header that you want tooread.</span></span> <span data-ttu-id="3dd27-163">Si no se incluye el encabezado de hello en solicitud de hello, el valor de hello será una cadena vacía Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-163">If hello header is not included on hello request, hello value will be hello empty string.</span></span>
* <span data-ttu-id="3dd27-164">**{request.querystring. \<ParameterName\>}**: un parámetro de cadena de consulta que se puede leer desde la solicitud original Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from hello original request.</span></span> <span data-ttu-id="3dd27-165">Reemplace  *\<ParameterName\>*  con nombre de Hola de parámetro de Hola que desea tooread.</span><span class="sxs-lookup"><span data-stu-id="3dd27-165">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooread.</span></span> <span data-ttu-id="3dd27-166">Si no se incluye el parámetro hello en solicitud de hello, el valor de hello será una cadena vacía Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-166">If hello parameter is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="3dd27-167"><a name="response-parameters"></a>Referencia a parámetros de respuesta de back-end</span><span class="sxs-lookup"><span data-stu-id="3dd27-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="3dd27-168">Parámetros de respuesta pueden utilizarse como parte de la modificación de cliente de toohello de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-168">Response parameters can be used as part of modifying hello response toohello client.</span></span> <span data-ttu-id="3dd27-169">Hola después valores puede utilizarse en los valores de configuración:</span><span class="sxs-lookup"><span data-stu-id="3dd27-169">hello following values can be used in config values:</span></span>

* <span data-ttu-id="3dd27-170">**{backend.response.statusCode}** : Hola código de estado HTTP que se devuelve en la respuesta de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-170">**{backend.response.statusCode}**: hello HTTP status code that's returned on hello back-end response.</span></span>
* <span data-ttu-id="3dd27-171">**{backend.response.statusReason}** : oración de motivo Hola HTTP que se devuelve en la respuesta de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-171">**{backend.response.statusReason}**: hello HTTP reason phrase that's returned on hello back-end response.</span></span>
* <span data-ttu-id="3dd27-172">**{backend.response.headers. \<HeaderName\>}**: un encabezado que puede leerse de respuesta de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from hello back-end response.</span></span> <span data-ttu-id="3dd27-173">Reemplace  *\<HeaderName\>*  con el nombre de hello del encabezado de hello desea tooread.</span><span class="sxs-lookup"><span data-stu-id="3dd27-173">Replace *\<HeaderName\>* with hello name of hello header you want tooread.</span></span> <span data-ttu-id="3dd27-174">Si no se incluye el encabezado de hello en solicitud de hello, el valor de hello será una cadena vacía Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-174">If hello header is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="3dd27-175"><a name="use-appsettings"></a>Referencia a la configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3dd27-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="3dd27-176">También puede hacer referencia a [configuración de la aplicación definida para la aplicación de la función de hello](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) rodeando el nombre de la configuración de hello con signos de porcentaje (%).</span><span class="sxs-lookup"><span data-stu-id="3dd27-176">You can also reference [application settings defined for hello function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding hello setting name with percent signs (%).</span></span>

<span data-ttu-id="3dd27-177">Por ejemplo, una URL de back-end de *https://%ORDER_PROCESSING_HOST%/api/orders* tendría "% ORDER_PROCESSING_HOST %" Reemplazar con valor de Hola de configuración de ORDER_PROCESSING_HOST de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with hello value of hello ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="3dd27-178">Use la configuración de la aplicación para hosts back-end si tiene varias implementaciones o entornos de prueba.</span><span class="sxs-lookup"><span data-stu-id="3dd27-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="3dd27-179">De este modo, puede asegurarse de que siempre están hablando toohello vuelta end para ese entorno.</span><span class="sxs-lookup"><span data-stu-id="3dd27-179">That way, you can make sure that you are always talking toohello right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="3dd27-180">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="3dd27-180">Advanced configuration</span></span>

<span data-ttu-id="3dd27-181">servidores proxy de Hola que configure se almacena en un archivo proxies.json, que se encuentra en la raíz de Hola de un directorio de aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="3dd27-181">hello proxies that you configure are stored in a proxies.json file, which is located in hello root of a function app directory.</span></span> <span data-ttu-id="3dd27-182">Puede editar este archivo manualmente e implementar como parte de la aplicación cuando se utiliza cualquiera de hello [métodos de implementación](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) compatible con las funciones.</span><span class="sxs-lookup"><span data-stu-id="3dd27-182">You can manually edit this file and deploy it as part of your app when you use any of hello [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="3dd27-183">característica de Hello debe ser [habilitado](#enable) para hello archivo toobe procesado.</span><span class="sxs-lookup"><span data-stu-id="3dd27-183">hello feature must be [enabled](#enable) for hello file toobe processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="3dd27-184">Si no configuró uno de los métodos de implementación de hello, también puede trabajar con archivos de proxies.json hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-184">If you have not set up one of hello deployment methods, you can also work with hello proxies.json file in hello portal.</span></span> <span data-ttu-id="3dd27-185">Aplicación de función vaya tooyour, seleccione **características de la plataforma**y, a continuación, seleccione **Editor de aplicación de servicio**.</span><span class="sxs-lookup"><span data-stu-id="3dd27-185">Go tooyour function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="3dd27-186">Al hacerlo, puede ver Hola estructura de archivo completo de la aplicación de la función y, a continuación, realizar cambios.</span><span class="sxs-lookup"><span data-stu-id="3dd27-186">By doing so, you can view hello entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="3dd27-187">El archivo proxies.json lo define un objeto de servidores proxy, compuesto de servidores proxy con nombre y de sus definiciones.</span><span class="sxs-lookup"><span data-stu-id="3dd27-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="3dd27-188">De forma opcional, si el editor lo admite, puede hacer referencia a un [esquema JSON](http://json.schemastore.org/proxies) para completar el código.</span><span class="sxs-lookup"><span data-stu-id="3dd27-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="3dd27-189">Un archivo de ejemplo podría ser similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="3dd27-189">An example file might look like hello following:</span></span>

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

<span data-ttu-id="3dd27-190">Cada proxy tiene un nombre descriptivo, como *proxy1* en el anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-190">Each proxy has a friendly name, such as *proxy1* in hello preceding example.</span></span> <span data-ttu-id="3dd27-191">objeto de definición de proxy correspondiente de Hola se define mediante Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="3dd27-191">hello corresponding proxy definition object is defined by hello following properties:</span></span>

* <span data-ttu-id="3dd27-192">**matchCondition**: obligatorio: un objeto que define las solicitudes de Hola que desencadenan la ejecución de Hola de este proxy.</span><span class="sxs-lookup"><span data-stu-id="3dd27-192">**matchCondition**: Required--an object defining hello requests that trigger hello execution of this proxy.</span></span> <span data-ttu-id="3dd27-193">Contiene dos propiedades compartidas con los [HTTP desencadenadores]:</span><span class="sxs-lookup"><span data-stu-id="3dd27-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="3dd27-194">_métodos_: una matriz de los métodos de hello HTTP que Hola proxy responde a.</span><span class="sxs-lookup"><span data-stu-id="3dd27-194">_methods_: An array of hello HTTP methods that hello proxy responds to.</span></span> <span data-ttu-id="3dd27-195">Si no se especifica, el proxy de Hola responde tooall métodos HTTP en la ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-195">If it is not specified, hello proxy responds tooall HTTP methods on hello route.</span></span>
    * <span data-ttu-id="3dd27-196">_ruta_: obligatorio: define la plantilla de ruta de hello, controlar que las direcciones URL de solicitud es el proxy responde a.</span><span class="sxs-lookup"><span data-stu-id="3dd27-196">_route_: Required--defines hello route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="3dd27-197">A diferencia de los desencadenadores HTTP, no hay ningún valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="3dd27-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="3dd27-198">**backendUri**: dirección URL de Hola Hola back-end toowhich Hola de solicitud de recursos debe ser procesadas por el proxy.</span><span class="sxs-lookup"><span data-stu-id="3dd27-198">**backendUri**: hello URL of hello back-end resource toowhich hello request should be proxied.</span></span> <span data-ttu-id="3dd27-199">Este valor puede hacer referencia a configuración de la aplicación y los parámetros de solicitud de cliente original Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-199">This value can reference application settings and parameters from hello original client request.</span></span> <span data-ttu-id="3dd27-200">Si no se incluye esta propiedad, Azure Functions responde con el mensaje HTTP 200 - Correcto.</span><span class="sxs-lookup"><span data-stu-id="3dd27-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="3dd27-201">**requestOverrides**: un objeto que define la solicitud de transformaciones toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="3dd27-201">**requestOverrides**: An object that defines transformations toohello back-end request.</span></span> <span data-ttu-id="3dd27-202">Consulte [definir un objeto requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="3dd27-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="3dd27-203">**responseOverrides**: un objeto que define la respuesta del cliente de toohello de transformaciones.</span><span class="sxs-lookup"><span data-stu-id="3dd27-203">**responseOverrides**: An object that defines transformations toohello client response.</span></span> <span data-ttu-id="3dd27-204">Consulte [definir un objeto responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="3dd27-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="3dd27-205">propiedad de ruta de Hello servidores proxy de las funciones de Azure no respeta la propiedad de hello routePrefix de configuración de host de las funciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-205">hello route property Azure Functions Proxies does not honor hello routePrefix property of hello Functions host configuration.</span></span> <span data-ttu-id="3dd27-206">Si desea tooinclude un prefijo, como/API, se deben incluirse en la propiedad de ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-206">If you want tooinclude a prefix such as /api, it must be included in hello route property.</span></span>

### <span data-ttu-id="3dd27-207"><a name="requestOverrides"></a>Definición de un objeto requestOverrides</span><span class="sxs-lookup"><span data-stu-id="3dd27-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="3dd27-208">objeto de Hello requestOverrides define cambios que realizó la solicitud de toohello cuando se llama a recursos de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-208">hello requestOverrides object defines changes made toohello request when hello back-end resource is called.</span></span> <span data-ttu-id="3dd27-209">objeto de Hola se define por hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="3dd27-209">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="3dd27-210">**backend.Request.Method**: Hola método HTTP que se ha utilizado toocall Hola back-end.</span><span class="sxs-lookup"><span data-stu-id="3dd27-210">**backend.request.method**: hello HTTP method that's used toocall hello back end.</span></span>
* <span data-ttu-id="3dd27-211">**backend.Request.QueryString. \<ParameterName\>**: un parámetro de cadena de consulta que se pueden establecer para hello llamada toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="3dd27-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for hello call toohello back end.</span></span> <span data-ttu-id="3dd27-212">Reemplace  *\<ParameterName\>*  con nombre de Hola de parámetro de Hola que desea tooset.</span><span class="sxs-lookup"><span data-stu-id="3dd27-212">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooset.</span></span> <span data-ttu-id="3dd27-213">Si se proporciona una cadena vacía hello, parámetro hello no se incluye en la solicitud de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-213">If hello empty string is provided, hello parameter is not included on hello back-end request.</span></span>
* <span data-ttu-id="3dd27-214">**backend.Request.Headers. \<HeaderName\>**: un encabezado que se pueden establecer para hello llamada toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="3dd27-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for hello call toohello back end.</span></span> <span data-ttu-id="3dd27-215">Reemplace  *\<HeaderName\>*  con nombre hello del encabezado de Hola que desea tooset.</span><span class="sxs-lookup"><span data-stu-id="3dd27-215">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="3dd27-216">Si proporciona una cadena vacía hello, encabezado de hello no se incluye en la solicitud de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-216">If you provide hello empty string, hello header is not included on hello back-end request.</span></span>

<span data-ttu-id="3dd27-217">Valores pueden hacer referencia a configuración de la aplicación y los parámetros de solicitud de cliente original Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-217">Values can reference application settings and parameters from hello original client request.</span></span>

<span data-ttu-id="3dd27-218">Una configuración de ejemplo podría ser similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="3dd27-218">An example configuration might look like hello following:</span></span>

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

### <span data-ttu-id="3dd27-219"><a name="responseOverrides"></a>Definición de un objeto responseOverrides</span><span class="sxs-lookup"><span data-stu-id="3dd27-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="3dd27-220">objeto requestOverrides de Hello define cambios que se realizan respuesta toohello que transcurrió a cliente toohello atrás.</span><span class="sxs-lookup"><span data-stu-id="3dd27-220">hello requestOverrides object defines changes that are made toohello response that's passed back toohello client.</span></span> <span data-ttu-id="3dd27-221">objeto de Hola se define por hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="3dd27-221">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="3dd27-222">**response.statusCode**: toobe de código de estado HTTP de hello devuelve toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="3dd27-222">**response.statusCode**: hello HTTP status code toobe returned toohello client.</span></span>
* <span data-ttu-id="3dd27-223">**response.statusReason**: Hola HTTP motivo frase toobe devuelve toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="3dd27-223">**response.statusReason**: hello HTTP reason phrase toobe returned toohello client.</span></span>
* <span data-ttu-id="3dd27-224">**Response.Body**: representación de cadena de Hola de hello cuerpo toobe devuelve toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="3dd27-224">**response.body**: hello string representation of hello body toobe returned toohello client.</span></span>
* <span data-ttu-id="3dd27-225">**Response.Headers. \<HeaderName\>**: un encabezado que puede establecer para hello respuesta toohello.</span><span class="sxs-lookup"><span data-stu-id="3dd27-225">**response.headers.\<HeaderName\>**: A header that can be set for hello response toohello client.</span></span> <span data-ttu-id="3dd27-226">Reemplace  *\<HeaderName\>*  con nombre hello del encabezado de Hola que desea tooset.</span><span class="sxs-lookup"><span data-stu-id="3dd27-226">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="3dd27-227">Si proporciona una cadena vacía hello, encabezado de hello no se incluye en la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-227">If you provide hello empty string, hello header is not included on hello response.</span></span>

<span data-ttu-id="3dd27-228">Valores pueden hacer referencia a configuración de la aplicación, los parámetros de solicitud de cliente original de Hola y los parámetros de respuesta de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dd27-228">Values can reference application settings, parameters from hello original client request, and parameters from hello back-end response.</span></span>

<span data-ttu-id="3dd27-229">Una configuración de ejemplo podría ser similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="3dd27-229">An example configuration might look like hello following:</span></span>

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
> <span data-ttu-id="3dd27-230">En este ejemplo, el cuerpo de hello es que se va a establecer directamente, por lo que no `backendUri` propiedad es necesaria.</span><span class="sxs-lookup"><span data-stu-id="3dd27-230">In this example, hello body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="3dd27-231">ejemplo de Hola muestra cómo puede usar a servidores proxy de las funciones de Azure para las API de simulación.</span><span class="sxs-lookup"><span data-stu-id="3dd27-231">hello example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

[portal de Azure]: https://portal.azure.com
[HTTP desencadenadores]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[definir un objeto requestOverrides]: #requestOverrides
[definir un objeto responseOverrides]: #responseOverrides
[configuración de la aplicación]: #use-appsettings
[Uso de variables]: #using-variables
[parámetros de solicitud de cliente original hello]: #request-parameters
[parámetros de respuesta de back-end de hello]: #response-parameters
