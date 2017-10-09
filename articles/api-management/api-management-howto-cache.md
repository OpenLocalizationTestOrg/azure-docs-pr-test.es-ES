---
title: "aaaAdd almacenamiento en caché tooimprove rendimiento en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo cargan la latencia de Hola de tooimprove, el consumo de ancho de banda y el servicio web de las llamadas de servicio de administración de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a><span data-ttu-id="087dd-103">Agregar almacenamiento en caché de tooimprove de rendimiento en la administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="087dd-103">Add caching tooimprove performance in Azure API Management</span></span>
<span data-ttu-id="087dd-104">En Administración de API, las operaciones se pueden configurar para el almacenamiento en caché de respuestas.</span><span class="sxs-lookup"><span data-stu-id="087dd-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="087dd-105">El almacenamiento en caché de respuestas puede reducir significativamente la latencia de la API, el consumo de ancho de banda y la carga del servicio web en cuanto a datos que no cambian con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="087dd-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="087dd-106">Esta guía le mostrará cómo tooadd respuesta configurar directivas para las operaciones de API de eco de ejemplo de Hola y almacenamiento en caché de la API.</span><span class="sxs-lookup"><span data-stu-id="087dd-106">This guide shows you how tooadd response caching for your API and configure policies for hello sample Echo API operations.</span></span> <span data-ttu-id="087dd-107">A continuación, puede llamar a operación hello en la caché de tooverify portal para desarrolladores de hello en acción.</span><span class="sxs-lookup"><span data-stu-id="087dd-107">You can then call hello operation from hello developer portal tooverify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="087dd-108">Para obtener información sobre el almacenamiento en caché de los elementos por parte de la clave mediante expresiones de directiva, consulte [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="087dd-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="087dd-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="087dd-109">Prerequisites</span></span>
<span data-ttu-id="087dd-110">Para los pasos siguiente hello en esta guía, debe tener una instancia de servicio de administración de API con una API y un producto configurado.</span><span class="sxs-lookup"><span data-stu-id="087dd-110">Before following hello steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="087dd-111">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="087dd-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="087dd-112"><a name="configure-caching"></a>Configuración de una operación para almacenamiento en caché</span><span class="sxs-lookup"><span data-stu-id="087dd-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="087dd-113">En este paso, revisará Hola almacenamiento en caché de configuración de hello **obtener recursos (en caché)** el funcionamiento de ejemplo de Hola a API de eco.</span><span class="sxs-lookup"><span data-stu-id="087dd-113">In this step, you will review hello caching settings of hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="087dd-114">Cada instancia de servicio de administración de API viene preconfigurado con una API de eco que se pueden tooexperiment usado con y obtener información acerca de la API de administración.</span><span class="sxs-lookup"><span data-stu-id="087dd-114">Each API Management service instance comes preconfigured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="087dd-115">Para más información, consulte [Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="087dd-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="087dd-116">tooget iniciado, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="087dd-116">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="087dd-117">Esto le llevará toohello portal para desarrolladores de administración de API.</span><span class="sxs-lookup"><span data-stu-id="087dd-117">This takes you toohello API Management publisher portal.</span></span>

![Portal del publicador][api-management-management-console]

<span data-ttu-id="087dd-119">Haga clic en **API** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **API de eco**.</span><span class="sxs-lookup"><span data-stu-id="087dd-119">Click **APIs** from hello **API Management** menu on hello left, and then click **Echo API**.</span></span>

![API eco][api-management-echo-api]

<span data-ttu-id="087dd-121">Haga clic en hello **Operations** ficha y, a continuación, haga clic en hello **obtener recursos (en caché)** operación de hello **Operations** lista.</span><span class="sxs-lookup"><span data-stu-id="087dd-121">Click hello **Operations** tab, and then click hello **GET Resource (cached)** operation from hello **Operations** list.</span></span>

![Echo API operations][api-management-echo-api-operations]

<span data-ttu-id="087dd-123">Haga clic en hello **Caching** Hola de tooview ficha almacenamiento en caché de configuración para esta operación.</span><span class="sxs-lookup"><span data-stu-id="087dd-123">Click hello **Caching** tab tooview hello caching settings for this operation.</span></span>

![Caching tab][api-management-caching-tab]

<span data-ttu-id="087dd-125">tooenable el almacenamiento en caché para una operación, seleccione hello **habilitar** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="087dd-125">tooenable caching for an operation, select hello **Enable** check box.</span></span> <span data-ttu-id="087dd-126">En este ejemplo, el almacenamiento en caché está habilitado.</span><span class="sxs-lookup"><span data-stu-id="087dd-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="087dd-127">Con una clave de cada respuesta de la operación, basándose en valores Hola Hola **variar por parámetros de cadena de consulta** y **variar por encabezados** campos.</span><span class="sxs-lookup"><span data-stu-id="087dd-127">Each operation response is keyed, based on hello values in hello **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="087dd-128">Si desea toocache varias respuestas en función de los parámetros de cadena de consulta o los encabezados, puede configurarlos en estos dos campos.</span><span class="sxs-lookup"><span data-stu-id="087dd-128">If you want toocache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="087dd-129">**Duración** especifica el intervalo de expiración de Hola de respuestas de hello en caché.</span><span class="sxs-lookup"><span data-stu-id="087dd-129">**Duration** specifies hello expiration interval of hello cached responses.</span></span> <span data-ttu-id="087dd-130">En este ejemplo, es el intervalo de saludo **3600** segundos, que es la hora tooone equivalente.</span><span class="sxs-lookup"><span data-stu-id="087dd-130">In this example, hello interval is **3600** seconds, which is equivalent tooone hour.</span></span>

<span data-ttu-id="087dd-131">Usar almacenamiento en caché de configuración en este ejemplo de Hola, Hola primer toohello de solicitud **obtener recursos (en caché)** operación devuelve una respuesta de servicio de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="087dd-131">Using hello caching configuration in this example, hello first request toohello **GET Resource (cached)** operation returns a response from hello backend service.</span></span> <span data-ttu-id="087dd-132">Esta respuesta se almacenarán en caché, ordenados por hello especificada parámetros de cadena de encabezados y la consulta.</span><span class="sxs-lookup"><span data-stu-id="087dd-132">This response will be cached, keyed by hello specified headers and query string parameters.</span></span> <span data-ttu-id="087dd-133">Las llamadas subsiguientes operación toohello, con la coincidencia de parámetros, tendrá hello en memoria caché respuesta devuelta, hasta que expire el intervalo de duración de caché de saludo.</span><span class="sxs-lookup"><span data-stu-id="087dd-133">Subsequent calls toohello operation, with matching parameters, will have hello cached response returned, until hello cache duration interval has expired.</span></span>

## <span data-ttu-id="087dd-134"><a name="caching-policies"></a>Hola revisión almacenamiento en caché de directivas</span><span class="sxs-lookup"><span data-stu-id="087dd-134"><a name="caching-policies"> </a>Review hello caching policies</span></span>
<span data-ttu-id="087dd-135">En este paso, revise Hola almacenamiento en caché de configuración de hello **obtener recursos (en caché)** el funcionamiento de ejemplo de Hola a API de eco.</span><span class="sxs-lookup"><span data-stu-id="087dd-135">In this step, you review hello caching settings for hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

<span data-ttu-id="087dd-136">Al almacenamiento en caché se configura para una operación en hello **Caching** ficha almacenamiento en caché de directivas se agregan para la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="087dd-136">When caching settings are configured for an operation on hello **Caching** tab, caching policies are added for hello operation.</span></span> <span data-ttu-id="087dd-137">Estas directivas pueden verse y modificarse en el editor de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="087dd-137">These policies can be viewed and edited in hello policy editor.</span></span>

<span data-ttu-id="087dd-138">Haga clic en **directivas** de hello **administración de API** menú Hola izquierda y, a continuación, seleccione **API eco / obtener los recursos (en caché)** de hello **operación**lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="087dd-138">Click **Policies** from hello **API Management** menu on hello left, and then select **Echo API / GET Resource (cached)** from hello **Operation** drop-down list.</span></span>

![Policy scope operation][api-management-operation-dropdown]

<span data-ttu-id="087dd-140">Esto muestra las directivas de Hola para esta operación en el editor de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="087dd-140">This displays hello policies for this operation in hello policy editor.</span></span>

![API Management policy editor][api-management-policy-editor]

<span data-ttu-id="087dd-142">definición de la directiva de Hola para esta operación incluye hello las directivas que definen Hola configuración de caché que se revisaron con hello **Caching** ficha en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="087dd-142">hello policy definition for this operation includes hello policies that define hello caching configuration that were reviewed using hello **Caching** tab in hello previous step.</span></span>

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> <span data-ttu-id="087dd-143">Almacenamiento en caché de directivas en el editor de directiva de Hola de toohello de los cambios realizados se reflejarán en hello **Caching** pestaña de una operación y viceversa.</span><span class="sxs-lookup"><span data-stu-id="087dd-143">Changes made toohello caching policies in hello policy editor will be reflected on hello **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="087dd-144"><a name="test-operation"></a>Llamar a una operación y probar el almacenamiento en caché de Hola</span><span class="sxs-lookup"><span data-stu-id="087dd-144"><a name="test-operation"> </a>Call an operation and test hello caching</span></span>
<span data-ttu-id="087dd-145">Hola toosee almacenamiento en caché en acción, podemos llamar operación Hola desde portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="087dd-145">toosee hello caching in action, we can call hello operation from hello developer portal.</span></span> <span data-ttu-id="087dd-146">Haga clic en **portal para desarrolladores de** en el menú superior derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="087dd-146">Click **Developer portal** in hello top right menu.</span></span>

![portal para desarrolladores][api-management-developer-portal-menu]

<span data-ttu-id="087dd-148">Haga clic en **API** en Hola menú superior y, a continuación, seleccione **API de eco**.</span><span class="sxs-lookup"><span data-stu-id="087dd-148">Click **APIs** in hello top menu, and then select **Echo API**.</span></span>

![API eco][api-management-apis-echo-api]

> <span data-ttu-id="087dd-150">Si tiene sólo una API configurada o cuenta tooyour visible, a continuación, haga clic en las API le lleva directamente operaciones toohello para la API.</span><span class="sxs-lookup"><span data-stu-id="087dd-150">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="087dd-151">Seleccione hello **obtener recursos (en caché)** operación y, a continuación, haga clic en **abrir la consola de**.</span><span class="sxs-lookup"><span data-stu-id="087dd-151">Select hello **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="087dd-153">Hola consola permite operaciones de tooinvoke directamente desde el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="087dd-153">hello console allows you tooinvoke operations directly from hello developer portal.</span></span>

![Consola][api-management-console]

<span data-ttu-id="087dd-155">Mantener valores predeterminados de Hola para **param1** y **param2**.</span><span class="sxs-lookup"><span data-stu-id="087dd-155">Keep hello default values for **param1** and **param2**.</span></span>

<span data-ttu-id="087dd-156">Seleccione Hola clave deseado de hello **clave de suscripción** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="087dd-156">Select hello desired key from hello **subscription-key** drop-down list.</span></span> <span data-ttu-id="087dd-157">Si su cuenta tiene solo una suscripción, ya estará seleccionada.</span><span class="sxs-lookup"><span data-stu-id="087dd-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="087dd-158">Escriba **sampleheader:value1** en hello **encabezados de solicitud** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="087dd-158">Enter **sampleheader:value1** in hello **Request headers** text box.</span></span>

<span data-ttu-id="087dd-159">Haga clic en **HTTP Get** y tome nota de hello encabezados de respuesta.</span><span class="sxs-lookup"><span data-stu-id="087dd-159">Click **HTTP Get** and make a note of hello response headers.</span></span>

<span data-ttu-id="087dd-160">Escriba **sampleheader:value2** en hello **encabezados de solicitud** cuadro de texto y, a continuación, haga clic en **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="087dd-160">Enter **sampleheader:value2** in hello **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="087dd-161">Tenga en cuenta ese valor Hola de **sampleheader** sigue siendo **value1** en respuesta Hola.</span><span class="sxs-lookup"><span data-stu-id="087dd-161">Note that hello value of **sampleheader** is still **value1** in hello response.</span></span> <span data-ttu-id="087dd-162">Pruebe algunos valores diferentes y tenga en cuenta que Hola respuesta almacenada en caché de la primera llamada de Hola se devuelve.</span><span class="sxs-lookup"><span data-stu-id="087dd-162">Try some different values and note that hello cached response from hello first call is returned.</span></span>

<span data-ttu-id="087dd-163">Escriba **25** en hello **param2** campo y, a continuación, haga clic en **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="087dd-163">Enter **25** into hello **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="087dd-164">Tenga en cuenta ese valor Hola de **sampleheader** en hello respuesta es ahora **value2**.</span><span class="sxs-lookup"><span data-stu-id="087dd-164">Note that hello value of **sampleheader** in hello response is now **value2**.</span></span> <span data-ttu-id="087dd-165">Porque los resultados de la operación de hello están organizados por cadena de consulta, no ha devuelto la respuesta almacenada en caché de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="087dd-165">Because hello operation results are keyed by query string, hello previous cached response was not returned.</span></span>

## <span data-ttu-id="087dd-166"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="087dd-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="087dd-167">Para obtener más información sobre el almacenamiento en caché de directivas, consulte [almacenamiento en caché de directivas de] [ Caching policies] en hello [referencia de directiva de administración de API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="087dd-167">For more information about caching policies, see [Caching policies][Caching policies] in hello [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="087dd-168">Para obtener información sobre el almacenamiento en caché de los elementos por parte de la clave mediante expresiones de directiva, consulte [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="087dd-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
