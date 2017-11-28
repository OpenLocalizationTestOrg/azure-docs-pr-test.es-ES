---
title: "aaaPolicies en administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo editar toocreate y configurar las directivas de administración de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="57062-103">Directivas de Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="57062-103">Policies in Azure API Management</span></span>
<span data-ttu-id="57062-104">En la administración de API de Azure, las directivas son una capacidad eficaz del sistema de Hola que permiten a publicador hello toochange comportamiento de Hola de hello API a través de la configuración.</span><span class="sxs-lookup"><span data-stu-id="57062-104">In Azure API Management, policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="57062-105">Las directivas son una colección de instrucciones que se ejecutan secuencialmente en la solicitud de Hola o respuesta de una API.</span><span class="sxs-lookup"><span data-stu-id="57062-105">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="57062-106">Las instrucciones más usadas incluyen la conversión de formato de XML tooJSON y llamar a la cantidad de hello toorestrict de llamadas entrantes de un desarrollador de limitación de velocidad.</span><span class="sxs-lookup"><span data-stu-id="57062-106">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="57062-107">Existen muchas más directivas desde el principio de Hola.</span><span class="sxs-lookup"><span data-stu-id="57062-107">Many more policies are available out of hello box.</span></span>

<span data-ttu-id="57062-108">Vea hello [referencia de directiva] [ Policy Reference] para obtener una lista completa de las instrucciones de directiva y su configuración.</span><span class="sxs-lookup"><span data-stu-id="57062-108">See hello [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="57062-109">Las directivas se aplican dentro de la puerta de enlace de Hola que se encuentra entre consumidor de la API de Hola y Hola managed API.</span><span class="sxs-lookup"><span data-stu-id="57062-109">Policies are applied inside hello gateway which sits between hello API consumer and hello managed API.</span></span> <span data-ttu-id="57062-110">recibe todas las solicitudes Hello puerta de enlace y normalmente reenvía sin modificaciones toohello subyacente API.</span><span class="sxs-lookup"><span data-stu-id="57062-110">hello gateway receives all requests and usually forwards them unaltered toohello underlying API.</span></span> <span data-ttu-id="57062-111">Sin embargo puede aplicar una directiva de solicitud entrante de cambios tooboth hello y respuesta saliente.</span><span class="sxs-lookup"><span data-stu-id="57062-111">However a policy can apply changes tooboth hello inbound request and outbound response.</span></span>

<span data-ttu-id="57062-112">Las expresiones de directiva se pueden usar como valores de atributo o valores de texto en cualquiera de las directivas de administración de API de hello, a menos que la directiva de Hola se especifique lo contrario.</span><span class="sxs-lookup"><span data-stu-id="57062-112">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="57062-113">Algunas directivas como hello [flujo de Control] [ Control flow] y [Set variable] [ Set variable] directivas basadas en expresiones de directiva.</span><span class="sxs-lookup"><span data-stu-id="57062-113">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="57062-114">Para obtener más información, consulte [Directivas avanzadas][Advanced policies] y [Expresiones de directiva][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="57062-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="57062-115"><a name="scopes"></a>Cómo tooconfigure directivas</span><span class="sxs-lookup"><span data-stu-id="57062-115"><a name="scopes"> </a>How tooconfigure policies</span></span>
<span data-ttu-id="57062-116">Las directivas se pueden configurar globalmente o en el ámbito de Hola de un [producto][Product], [API] [ API] o [operación] [Operation].</span><span class="sxs-lookup"><span data-stu-id="57062-116">Policies can be configured globally or at hello scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="57062-117">tooconfigure una directiva, navegue toohello editor de directivas en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="57062-117">tooconfigure a policy, navigate toohello Policies editor in hello publisher portal.</span></span>

![Policies menu][policies-menu]

<span data-ttu-id="57062-119">el editor de directivas de Hello consta de tres secciones principales: Hola ámbito (superior), Hola directiva definición de directiva donde las directivas se editan (izquierda) y las instrucciones de hello lista (derecha):</span><span class="sxs-lookup"><span data-stu-id="57062-119">hello policies editor consists of three main sections: hello policy scope (top), hello policy definition where policies are edited (left) and hello statements list (right):</span></span>

![Policies editor][policies-editor]

<span data-ttu-id="57062-121">toobegin configurar una directiva que primero debe seleccionar ámbito de hello en qué Hola debe aplicarse la directiva.</span><span class="sxs-lookup"><span data-stu-id="57062-121">toobegin configuring a policy you must first select hello scope at which hello policy should apply.</span></span> <span data-ttu-id="57062-122">En la captura de pantalla de hello siguiente hello **Starter** producto se selecciona.</span><span class="sxs-lookup"><span data-stu-id="57062-122">In hello screenshot below hello **Starter** product is selected.</span></span> <span data-ttu-id="57062-123">Tenga en cuenta que este nombre de directiva Hola símbolo cuadrado siguiente toohello indica que ya se aplica una directiva en este nivel.</span><span class="sxs-lookup"><span data-stu-id="57062-123">Note that hello square symbol next toohello policy name indicates that a policy is already applied at this level.</span></span>

![Scope][policies-scope]

<span data-ttu-id="57062-125">Puesto que ya se ha aplicado una directiva, configuración de Hola se muestra en la vista de definición de Hola.</span><span class="sxs-lookup"><span data-stu-id="57062-125">Since a policy has already been applied, hello configuration is shown in hello definition view.</span></span>

![Configuración][policies-configure]

<span data-ttu-id="57062-127">Hola directiva se muestra como de solo lectura en un primer momento.</span><span class="sxs-lookup"><span data-stu-id="57062-127">hello policy is displayed read-only at first.</span></span> <span data-ttu-id="57062-128">En orden tooedit definición hello, haga clic en hello **Configurar directiva** acción.</span><span class="sxs-lookup"><span data-stu-id="57062-128">In order tooedit hello definition click hello **Configure Policy** action.</span></span>

![Edit][policies-edit]

<span data-ttu-id="57062-130">definición de la directiva de Hello es un documento XML sencillo que describe una secuencia de instrucciones entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="57062-130">hello policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="57062-131">Hola XML puede modificarse directamente en la ventana de definición de hello.</span><span class="sxs-lookup"><span data-stu-id="57062-131">hello XML can be edited directly in hello definition window.</span></span> <span data-ttu-id="57062-132">Una lista de instrucciones es siempre toohello derecha y el ámbito actual de instrucciones toohello aplicables están habilitados y resaltados; como se muestra en hello **límite de velocidad de llamar a** instrucción de captura de pantalla de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="57062-132">A list of statements is provided toohello right and statements applicable toohello current scope are enabled and highlighted; as demonstrated by hello **Limit Call Rate** statement in hello screenshot above.</span></span>

<span data-ttu-id="57062-133">Al hacer clic en una instrucción habilitada agregará Hola código XML adecuado en la ubicación de Hola de cursor de hello en la vista de definición de Hola.</span><span class="sxs-lookup"><span data-stu-id="57062-133">Clicking an enabled statement will add hello appropriate XML at hello location of hello cursor in hello definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="57062-134">Si no está habilitada la directiva de Hola que desea tooadd, asegúrese de que está en el ámbito correcto de saludo de la directiva.</span><span class="sxs-lookup"><span data-stu-id="57062-134">If hello policy that you want tooadd is not enabled, ensure that you are in hello correct scope for that policy.</span></span> <span data-ttu-id="57062-135">Cada instrucción de la directiva está diseñada para su uso en determinados ámbitos y secciones de la directiva.</span><span class="sxs-lookup"><span data-stu-id="57062-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="57062-136">secciones de la directiva de tooreview hello y ámbitos para una directiva, compruebe hello **uso** sección de la directiva en hello [referencia de directiva][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="57062-136">tooreview hello policy sections and scopes for a policy, check hello **Usage** section for that policy in hello [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="57062-137">Una lista completa de las instrucciones de directiva y sus valores están disponibles en hello [referencia de directiva][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="57062-137">A full list of policy statements and their settings are available in hello [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="57062-138">Por ejemplo, tooadd un nuevo toorestrict de instrucción entrante solicita toospecified las direcciones IP, coloque Hola cursor solo en el contenido de Hola de hello `inbound` Hola de elemento y haga clic en XML **llamador restringir IP** instrucción.</span><span class="sxs-lookup"><span data-stu-id="57062-138">For example, tooadd a new statement toorestrict incoming requests toospecified IP addresses, place hello cursor just inside hello content of hello `inbound` XML element and click hello **Restrict caller IPs** statement.</span></span>

![Restriction policies][policies-restrict]

<span data-ttu-id="57062-140">Esto agregará una toohello de fragmento de código XML `inbound` elemento que se proporciona instrucciones sobre cómo tooconfigure Hola instrucción.</span><span class="sxs-lookup"><span data-stu-id="57062-140">This will add an XML snippet toohello `inbound` element that provides guidance on how tooconfigure hello statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="57062-141">toolimit las solicitudes de entrada y Aceptar sólo aquellos desde una dirección IP de 1.2.3.4 modificar Hola XML como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="57062-141">toolimit inbound requests and accept only those from an IP address of 1.2.3.4 modify hello XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Save][policies-save]

<span data-ttu-id="57062-143">Cuando se complete configuración instrucciones Hola de directiva de hello, haga clic en **guardar** y cambios de hello será puerta de enlace de administración de API toohello propagado inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="57062-143">When complete configuring hello statements for hello policy, click **Save** and hello changes will be propagated toohello API Management gateway immediately.</span></span>

## <span data-ttu-id="57062-144"><a name="sections"></a>Descripción de la configuración de directivas</span><span class="sxs-lookup"><span data-stu-id="57062-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="57062-145">Una directiva es una serie de declaraciones que se ejecutan en orden para una solicitud y una respuesta.</span><span class="sxs-lookup"><span data-stu-id="57062-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="57062-146">configuración de Hola se divide adecuadamente en `inbound`, `backend`, `outbound`, y `on-error` secciones tal y como se muestra en la siguiente configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="57062-146">hello configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in hello following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="57062-147">Si se produce un error durante el procesamiento de Hola de una solicitud, los pasos restantes hello `inbound`, `backend`, o `outbound` secciones se omiten y ejecución saltará instrucciones toohello Hola `on-error` sección.</span><span class="sxs-lookup"><span data-stu-id="57062-147">If there is an error during hello processing of a request, any remaining steps in hello `inbound`, `backend`, or `outbound` sections are skipped and execution jumps toohello statements in hello `on-error` section.</span></span> <span data-ttu-id="57062-148">Mediante la colocación de las instrucciones de directiva en hello `on-error` sección podrá revisar error hello mediante hello `context.LastError` propiedad, inspeccionar y personalizar la respuesta de error de hello mediante hello `set-body` directiva y configurar lo que ocurre si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="57062-148">By placing policy statements in hello `on-error` section you can review hello error by using hello `context.LastError` property, inspect and customize hello error response using hello `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="57062-149">Hay códigos de error para conocer los pasos integrados y los errores que pueden producirse durante el procesamiento de Hola de las instrucciones de directiva.</span><span class="sxs-lookup"><span data-stu-id="57062-149">There are error codes for built-in steps and for errors that may occur during hello processing of policy statements.</span></span> <span data-ttu-id="57062-150">Para más información, consulte [Control de errores en las directivas de administración de API](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="57062-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="57062-151">Puesto que las directivas se pueden especificar en diferentes niveles (global, producto, api y operación) configuración Hola proporciona una manera para usted toospecify orden de hello en la que se ejecutan las instrucciones de definición de la directiva de hello con la directiva de respeto toohello primario.</span><span class="sxs-lookup"><span data-stu-id="57062-151">Since policies can be specified at different levels (global, product, api and operation) hello configuration provides a way for you toospecify hello order in which hello policy definition's statements execute with respect toohello parent policy.</span></span> 

<span data-ttu-id="57062-152">Ámbitos de la directiva se evalúan en hello siguiendo el orden.</span><span class="sxs-lookup"><span data-stu-id="57062-152">Policy scopes are evaluated in hello following order.</span></span>

1. <span data-ttu-id="57062-153">Ámbito global</span><span class="sxs-lookup"><span data-stu-id="57062-153">Global scope</span></span>
2. <span data-ttu-id="57062-154">Ámbito del producto</span><span class="sxs-lookup"><span data-stu-id="57062-154">Product scope</span></span>
3. <span data-ttu-id="57062-155">Ámbito de la API</span><span class="sxs-lookup"><span data-stu-id="57062-155">API scope</span></span>
4. <span data-ttu-id="57062-156">Ámbito de la operación</span><span class="sxs-lookup"><span data-stu-id="57062-156">Operation scope</span></span>

<span data-ttu-id="57062-157">Hello dentro de ellos se evalúen las instrucciones según la selección de ubicación de toohello de hello `base` elemento, si está presente.</span><span class="sxs-lookup"><span data-stu-id="57062-157">hello statements within them are evaluated according toohello placement of hello `base` element, if it is present.</span></span> <span data-ttu-id="57062-158">Directiva global tiene ninguna directiva de elemento primario y el uso de hello `<base>` elemento en el no tiene ningún efecto.</span><span class="sxs-lookup"><span data-stu-id="57062-158">Global policy has no parent policy and using hello `<base>` element in it has no effect.</span></span>

<span data-ttu-id="57062-159">Por ejemplo, si tiene una directiva en el nivel global de hello y una directiva configurada para una API, a continuación, cada vez que se utiliza esa API determinada las dos directivas se aplicará.</span><span class="sxs-lookup"><span data-stu-id="57062-159">For example, if you have a policy at hello global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="57062-160">Administración de API permite orden determinista de las instrucciones de directiva combinada a través del elemento base Hola.</span><span class="sxs-lookup"><span data-stu-id="57062-160">API Management allows for deterministic ordering of combined policy statements via hello base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="57062-161">En hello ejemplo definición de directiva anterior, Hola `cross-domain` ejecutaría instrucción antes de que las directivas de mayor que tomaría a su vez, ir seguido de hello `find-and-replace` directiva.</span><span class="sxs-lookup"><span data-stu-id="57062-161">In hello example policy definition above, hello `cross-domain` statement would execute before any higher policies which would in turn, be followed by hello `find-and-replace` policy.</span></span> 

<span data-ttu-id="57062-162">directivas de hello toosee en el ámbito actual de hello en el editor de directiva de hello, haga clic en **recalcular directiva en vigor para el ámbito seleccionado**.</span><span class="sxs-lookup"><span data-stu-id="57062-162">toosee hello policies in hello current scope in hello policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57062-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="57062-163">Next steps</span></span>
<span data-ttu-id="57062-164">Visualice el siguiente vídeo acerca de expresiones de directivas.</span><span class="sxs-lookup"><span data-stu-id="57062-164">Check out following video on policy expressions.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
