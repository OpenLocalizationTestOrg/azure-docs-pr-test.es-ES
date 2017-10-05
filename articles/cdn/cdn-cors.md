---
title: Uso de la red CDN de Azure con CORS | Microsoft Docs
description: "Descubra cómo usar la red de entrega de contenido (CDN) de Azure con el Uso compartido de recursos entre orígenes (CORS)."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7070397f6e69b21add75bad8220f0b8ebe36d266
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="8000e-103">Uso de la red CDN de Azure con CORS</span><span class="sxs-lookup"><span data-stu-id="8000e-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="8000e-104">¿Qué es CORS?</span><span class="sxs-lookup"><span data-stu-id="8000e-104">What is CORS?</span></span>
<span data-ttu-id="8000e-105">CORS (Uso compartido de recursos entre orígenes) es una característica de HTTP que permite que una aplicación web que se ejecuta en un dominio tenga acceso a recursos de otro dominio.</span><span class="sxs-lookup"><span data-stu-id="8000e-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain.</span></span> <span data-ttu-id="8000e-106">Para reducir la posibilidad de ataques de scripts de sitios, todos los exploradores web modernos implementan una restricción de seguridad que se conoce como [directiva del mismo origen](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="8000e-106">In order to reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="8000e-107">Esto impide que una página web llame a las API de un dominio distinto.</span><span class="sxs-lookup"><span data-stu-id="8000e-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="8000e-108">CORS aporta un modo seguro de permitir que un origen (el dominio de origen) llame a las API de otro origen.</span><span class="sxs-lookup"><span data-stu-id="8000e-108">CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="8000e-109">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="8000e-109">How it works</span></span>
<span data-ttu-id="8000e-110">Hay dos tipos de solicitudes de CORS, *solicitudes sencillas* y *solicitudes complejas.*</span><span class="sxs-lookup"><span data-stu-id="8000e-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="8000e-111">Para solicitudes sencillas:</span><span class="sxs-lookup"><span data-stu-id="8000e-111">For simple requests:</span></span>

1. <span data-ttu-id="8000e-112">El explorador envía la solicitud de CORS con un encabezado de solicitud HTTP de **origen** adicional.</span><span class="sxs-lookup"><span data-stu-id="8000e-112">The browser sends the CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="8000e-113">El valor de este encabezado es el origen del que proviene la página primaria, que se define como la combinación de *protocolo,* *dominio,* y *puerto.*</span><span class="sxs-lookup"><span data-stu-id="8000e-113">The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="8000e-114">Cuando una página de https://www.contoso.com intenta acceder a datos de un usuario en el origen fabrikam.com, se envía el siguiente encabezado de solicitud a fabrikam.com:</span><span class="sxs-lookup"><span data-stu-id="8000e-114">When a page from https://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="8000e-115">El servidor puede responder con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8000e-115">The server may respond with any of the following:</span></span>

   * <span data-ttu-id="8000e-116">Un encabezado **Access-Control-Allow-Origin** en la respuesta, que indica cuál de los sitios de origen se permite.</span><span class="sxs-lookup"><span data-stu-id="8000e-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="8000e-117">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8000e-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="8000e-118">Un código de error HTTP como el 403 si el servidor no permite la solicitud de origen cruzado después de comprobar el encabezado de origen</span><span class="sxs-lookup"><span data-stu-id="8000e-118">An HTTP error code such as 403 if the server does not allow the cross-origin request after checking the Origin header</span></span>

   * <span data-ttu-id="8000e-119">Un encabezado **Access-Control-Allow-Origin** con un carácter comodín que permite todos los dominios:</span><span class="sxs-lookup"><span data-stu-id="8000e-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="8000e-120">Para solicitudes complejas:</span><span class="sxs-lookup"><span data-stu-id="8000e-120">For complex requests:</span></span>

<span data-ttu-id="8000e-121">Una solicitud compleja es una solicitud de CORS en la que es necesario que el explorador envíe una *solicitud preparatoria* (es decir, un sondeo preliminar) antes de enviar la solicitud de CORS real.</span><span class="sxs-lookup"><span data-stu-id="8000e-121">A complex request is a CORS request where the browser is required to send a *preflight request* (i.e. a preliminary probe) before sending the actual CORS request.</span></span> <span data-ttu-id="8000e-122">La solicitud preparatoria solicita el permiso de servidor si la solicitud de CORS original puede continuar y es una solicitud `OPTIONS` a la misma dirección URL.</span><span class="sxs-lookup"><span data-stu-id="8000e-122">The preflight request asks the server permission if the original CORS request can proceed and is an `OPTIONS` request to the same URL.</span></span>

> [!TIP]
> <span data-ttu-id="8000e-123">Para obtener más detalles sobre los flujos de CORS y los errores comunes, consulte la [guía de CORS para las API de REST](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="8000e-123">For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="8000e-124">Escenarios de origen único o carácter comodín</span><span class="sxs-lookup"><span data-stu-id="8000e-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="8000e-125">En la red CDN de Azure, CORS funcionará automáticamente sin ninguna configuración adicional, cuando el encabezado **Access-Control-Allow-Origin** esté establecido en un carácter comodín (*) o en un solo origen.</span><span class="sxs-lookup"><span data-stu-id="8000e-125">CORS on Azure CDN will work automatically with no additional configuration when the **Access-Control-Allow-Origin** header is set to wildcard (*) or a single origin.</span></span>  <span data-ttu-id="8000e-126">La red CDN copiará en caché la primera respuesta, y las solicitudes siguientes usarán el mismo encabezado.</span><span class="sxs-lookup"><span data-stu-id="8000e-126">The CDN will cache the first response and subsequent requests will use the same header.</span></span>

<span data-ttu-id="8000e-127">Si ya se han enviado solicitudes a la red CDN antes de establecer CORS en el origen, tendrá que purgar el contenido del punto de conexión para volver a cargarlo con el encabezado **Access-Control-Allow-Origin** .</span><span class="sxs-lookup"><span data-stu-id="8000e-127">If requests have already been made to the CDN prior to CORS being set on the your origin, you will need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="8000e-128">Escenarios de varios orígenes</span><span class="sxs-lookup"><span data-stu-id="8000e-128">Multiple origin scenarios</span></span>
<span data-ttu-id="8000e-129">Si necesita permitir una lista específica de orígenes admitidos para CORS, el proceso puede resultar un poco más complicado.</span><span class="sxs-lookup"><span data-stu-id="8000e-129">If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="8000e-130">Encontramos el primer problema cuando la red CDN copia en caché el encabezado **Access-Control-Allow-Origin** el primer origen de CORS.</span><span class="sxs-lookup"><span data-stu-id="8000e-130">The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin.</span></span>  <span data-ttu-id="8000e-131">Cuando un origen de CORS distinto realiza una solicitud posteriormente, la red CDN enviará el encabezado **Access-Control-Allow-Origin** copiado en la caché, que no coincidirá.</span><span class="sxs-lookup"><span data-stu-id="8000e-131">When a different CORS origin makes a subsequent request, the CDN will serve the cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="8000e-132">Existen diversas formas de corregir este problema.</span><span class="sxs-lookup"><span data-stu-id="8000e-132">There are several ways to correct this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="8000e-133">Red CDN premium de Azure de Verizon</span><span class="sxs-lookup"><span data-stu-id="8000e-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="8000e-134">La mejor forma de habilitarlo es usar la **red CDN premium de Azure de Verizon**, que expone una serie de funciones avanzadas.</span><span class="sxs-lookup"><span data-stu-id="8000e-134">The best way to enable this is to use **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="8000e-135">Tendrá que [crear una regla](cdn-rules-engine.md) para comprobar encabezado **Origin** de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="8000e-135">You'll need to [create a rule](cdn-rules-engine.md) to check the **Origin** header on the request.</span></span>  <span data-ttu-id="8000e-136">Si se trata de un origen válido, la regla establecerá el encabezado **Access-Control-Allow-Origin** con el origen proporcionado en la solicitud.</span><span class="sxs-lookup"><span data-stu-id="8000e-136">If it's a valid origin, your rule will set the **Access-Control-Allow-Origin** header with the origin provided in the request.</span></span>  <span data-ttu-id="8000e-137">Si el origen especificado en el encabezado **Origin** no se permite, la regla tendrá que omitir el encabezado **Access-Control-Allow-Origin** que ocasionará que el explorador rechace la solicitud.</span><span class="sxs-lookup"><span data-stu-id="8000e-137">If the origin specified in the **Origin** header is not allowed, your rule should omit the **Access-Control-Allow-Origin** header which will cause the browser to reject the request.</span></span> 

<span data-ttu-id="8000e-138">Hay dos formas de hacerlo con el motor de reglas.</span><span class="sxs-lookup"><span data-stu-id="8000e-138">There are two ways to do this with the rules engine.</span></span>  <span data-ttu-id="8000e-139">En ambos casos, el encabezado **Access-Control-Allow-Origin** del servidor de origen del archivo se pasa por alto completamente; el motor de reglas de la red CDN administra totalmente los orígenes de CORS admitidos.</span><span class="sxs-lookup"><span data-stu-id="8000e-139">In both cases, the **Access-Control-Allow-Origin** header from the file's origin server is completely ignored, the CDN's rules engine completely manages the allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="8000e-140">Una expresión regular con todos los orígenes válidos</span><span class="sxs-lookup"><span data-stu-id="8000e-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="8000e-141">En este caso, creará una expresión regular en la que incluirá todos los orígenes que desea permitir:</span><span class="sxs-lookup"><span data-stu-id="8000e-141">In this case, you'll create a regular expression that includes all of the origins you want to allow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="8000e-142">**red CDN de Azure de Verizon** utiliza las [expresiones regulares compatibles con Perl](http://pcre.org/) como su motor de expresiones regulares.</span><span class="sxs-lookup"><span data-stu-id="8000e-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="8000e-143">Puede usar una herramienta como [Regular Expressions 101](https://regex101.com/) para validar la expresión regular.</span><span class="sxs-lookup"><span data-stu-id="8000e-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) to validate your regular expression.</span></span>  <span data-ttu-id="8000e-144">Tenga en cuenta que el carácter "/" es válido en expresiones regulares y no hace falta darle formato de escape; sin embargo, darle dicho formato se considera el procedimiento recomendado y algunos validadores de expresiones regulares lo esperan.</span><span class="sxs-lookup"><span data-stu-id="8000e-144">Note that the "/" character is valid in regular expressions and doesn't need to be escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="8000e-145">Si la expresión regular coincide, la regla reemplazará el encabezado **Access-Control-Allow-Origin** (en caso de haber alguno) del origen por el origen que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="8000e-145">If the regular expression matches, your rule will replace the **Access-Control-Allow-Origin** header (if any) from the origin with the origin that sent the request.</span></span>  <span data-ttu-id="8000e-146">También puede añadir encabezados de CORS adicionales, como **Access-Control-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="8000e-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Ejemplo de reglas con expresiones regulares](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="8000e-148">Regla de encabezado de solicitud para cada origen</span><span class="sxs-lookup"><span data-stu-id="8000e-148">Request header rule for each origin.</span></span>
<span data-ttu-id="8000e-149">En lugar de usar expresiones regulares, puede crear una regla aparte para cada origen que quiera permitir con la **condición de coincidencia** [carácter comodín del encabezado de solicitud](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="8000e-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish to allow using the **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="8000e-150">Al igual que con el método de expresión regular, el motor de reglas es el único que establece los encabezados de CORS.</span><span class="sxs-lookup"><span data-stu-id="8000e-150">As with the regular expression method, the rules engine alone sets the CORS headers.</span></span> 

![Ejemplo de reglas sin expresiones regulares](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="8000e-152">En el ejemplo anterior, el uso del carácter comodín * indica al motor de reglas que se admiten tanto HTTP como HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8000e-152">In the example above, the use of the wildcard character * tells the rules engine to match both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="8000e-153">Estándar de red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="8000e-153">Azure CDN Standard</span></span>
<span data-ttu-id="8000e-154">En los perfiles estándar de la red CDN de Azure, el único mecanismo para permitir varios orígenes sin usar el carácter comodín consiste en utilizar el [almacenamiento en caché de la cadena de consulta](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="8000e-154">On Azure CDN Standard profiles, the only mechanism to allow for multiple origins without the use of the wildcard origin is to use [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="8000e-155">Debe habilitar la configuración de la cadena de consulta para el punto de conexión de la red CDN y, después, utilizar una cadena de consulta única para las solicitudes de cada dominio permitido.</span><span class="sxs-lookup"><span data-stu-id="8000e-155">You need to enable query string setting for the CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="8000e-156">De este modo, la red CDN copiará en caché un objeto independiente para cada cadena de consulta única.</span><span class="sxs-lookup"><span data-stu-id="8000e-156">Doing this will result in the CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="8000e-157">Sin embargo, este enfoque no es ideal, ya que conllevará varias copias del mismo archivo en caché en la red CDN.</span><span class="sxs-lookup"><span data-stu-id="8000e-157">This approach is not ideal, however, as it will result in multiple copies of the same file cached on the CDN.</span></span>  

