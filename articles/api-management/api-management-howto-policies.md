---
title: Directivas de Azure API Management | Microsoft Docs
description: "Obtenga información acerca de cómo crear, editar y configurar directivas en Administración de API."
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
ms.openlocfilehash: 7c1f235343074ec11c635097f2b094a10f3fe781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="9c7d9-103">Directivas de Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="9c7d9-103">Policies in Azure API Management</span></span>
<span data-ttu-id="9c7d9-104">En Administración de API de Azure, las directivas constituyen una eficaz funcionalidad del sistema que permite al editor cambiar el comportamiento de la API a través de la configuración.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-104">In Azure API Management, policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="9c7d9-105">Las directivas son una colección de declaraciones que se ejecutan secuencialmente en la solicitud o respuesta de una API.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-105">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="9c7d9-106">Entre las declaraciones más usadas se encuentran la conversión de formato de XML a JSON y la limitación de tasa de llamadas para restringir la cantidad de llamadas entrantes de un desarrollador.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-106">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="9c7d9-107">Hay muchas más directivas disponibles y listas para usar.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-107">Many more policies are available out of the box.</span></span>

<span data-ttu-id="9c7d9-108">Consulte la [referencia de directivas][Policy Reference] para obtener una lista de declaraciones de directiva con su configuración.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-108">See the [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="9c7d9-109">Las directivas se aplican en la puerta de enlace que se encuentra entre el consumidor de la API y la API administrada.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-109">Policies are applied inside the gateway which sits between the API consumer and the managed API.</span></span> <span data-ttu-id="9c7d9-110">La puerta de enlace recibe todas las solicitudes y normalmente las reenvía sin modificar a la API subyacente.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-110">The gateway receives all requests and usually forwards them unaltered to the underlying API.</span></span> <span data-ttu-id="9c7d9-111">Sin embargo, una directiva puede aplicar cambios a la solicitud de entrada y a la respuesta de salida.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-111">However a policy can apply changes to both the inbound request and outbound response.</span></span>

<span data-ttu-id="9c7d9-112">Las expresiones de directiva pueden utilizarse como valores de atributos o valores de texto en cualquiera de las directivas de Administración de API, a menos que la directiva especifique lo contrario.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-112">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="9c7d9-113">Algunas directivas como [Flujo de control][Control flow] y [Establecer variable][Set variable] se basan en expresiones de directiva.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-113">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="9c7d9-114">Para obtener más información, consulte [Directivas avanzadas][Advanced policies] y [Expresiones de directiva][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="9c7d9-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="9c7d9-115"><a name="scopes"> </a>Configuración de directivas</span><span class="sxs-lookup"><span data-stu-id="9c7d9-115"><a name="scopes"> </a>How to configure policies</span></span>
<span data-ttu-id="9c7d9-116">Las directivas se pueden configurar globalmente o en el ámbito de un [producto][Product], una [API][API] o una [operación][Operation].</span><span class="sxs-lookup"><span data-stu-id="9c7d9-116">Policies can be configured globally or at the scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="9c7d9-117">Para configurar una directiva, vaya al editor de directivas del portal de publicadores.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-117">To configure a policy, navigate to the Policies editor in the publisher portal.</span></span>

![Policies menu][policies-menu]

<span data-ttu-id="9c7d9-119">El editor de directivas consta de tres secciones principales: el ámbito de la directiva (superior), la definición de la directiva donde se editan las directivas (izquierda) y la lista de instrucciones (derecha):</span><span class="sxs-lookup"><span data-stu-id="9c7d9-119">The policies editor consists of three main sections: the policy scope (top), the policy definition where policies are edited (left) and the statements list (right):</span></span>

![Policies editor][policies-editor]

<span data-ttu-id="9c7d9-121">Para comenzar a configurar una directiva, se debe seleccionar en primer lugar el ámbito en el que se debe aplicar.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-121">To begin configuring a policy you must first select the scope at which the policy should apply.</span></span> <span data-ttu-id="9c7d9-122">En la captura de pantalla siguiente, se selecciona el producto **Starter** .</span><span class="sxs-lookup"><span data-stu-id="9c7d9-122">In the screenshot below the **Starter** product is selected.</span></span> <span data-ttu-id="9c7d9-123">Tenga en cuenta que el símbolo de recuadro junto al nombre de la directiva indica que ya se aplica una directiva en este nivel.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-123">Note that the square symbol next to the policy name indicates that a policy is already applied at this level.</span></span>

![Scope][policies-scope]

<span data-ttu-id="9c7d9-125">Puesto que ya se ha aplicado una directiva, la configuración se muestra en la vista de definición.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-125">Since a policy has already been applied, the configuration is shown in the definition view.</span></span>

![Configuración][policies-configure]

<span data-ttu-id="9c7d9-127">La directiva aparece como de solo lectura al principio.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-127">The policy is displayed read-only at first.</span></span> <span data-ttu-id="9c7d9-128">Para editar la definición, haga clic en la acción **Configurar directiva** .</span><span class="sxs-lookup"><span data-stu-id="9c7d9-128">In order to edit the definition click the **Configure Policy** action.</span></span>

![Edit][policies-edit]

<span data-ttu-id="9c7d9-130">La definición de la directiva es un documento XML simple que describe una secuencia de declaraciones de entrada y de salida.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-130">The policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="9c7d9-131">El XML se puede editar directamente en la ventana de definición.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-131">The XML can be edited directly in the definition window.</span></span> <span data-ttu-id="9c7d9-132">Se ofrece una lista de instrucciones a la derecha y las instrucciones aplicables al ámbito actual están habilitadas y resaltadas; como demuestra la instrucción **Límite de tasa de llamadas** de la captura de pantalla anterior.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-132">A list of statements is provided to the right and statements applicable to the current scope are enabled and highlighted; as demonstrated by the **Limit Call Rate** statement in the screenshot above.</span></span>

<span data-ttu-id="9c7d9-133">Al hacer clic en una declaración habilitada se agregará el XML correspondiente en la ubicación del cursor en la vista de definición.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-133">Clicking an enabled statement will add the appropriate XML at the location of the cursor in the definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="9c7d9-134">Si la directiva que desea agregar no está habilitada, asegúrese de que se encuentra en el ámbito correcto para esa directiva.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-134">If the policy that you want to add is not enabled, ensure that you are in the correct scope for that policy.</span></span> <span data-ttu-id="9c7d9-135">Cada instrucción de la directiva está diseñada para su uso en determinados ámbitos y secciones de la directiva.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="9c7d9-136">Para revisar las secciones y los ámbitos de una directiva, compruebe la sección de **uso** de esa directiva en la [referencia de directivas][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="9c7d9-136">To review the policy sections and scopes for a policy, check the **Usage** section for that policy in the [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="9c7d9-137">Hay una lista completa de instrucciones de directivas y su configuración disponible en la [referencia de directivas][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="9c7d9-137">A full list of policy statements and their settings are available in the [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="9c7d9-138">Por ejemplo, para agregar una nueva instrucción a fin de restringir las solicitudes de entrada a las direcciones IP especificadas, sitúe el cursor exactamente dentro del contenido del elemento XLM `inbound` y haga clic en la instrucción **Restringir las IP del autor de llamada** .</span><span class="sxs-lookup"><span data-stu-id="9c7d9-138">For example, to add a new statement to restrict incoming requests to specified IP addresses, place the cursor just inside the content of the `inbound` XML element and click the **Restrict caller IPs** statement.</span></span>

![Restriction policies][policies-restrict]

<span data-ttu-id="9c7d9-140">Así, se agregará un fragmento de código XML al elemento `inbound` que ofrece orientación sobre cómo configurar la instrucción.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-140">This will add an XML snippet to the `inbound` element that provides guidance on how to configure the statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="9c7d9-141">Para limitar las solicitudes de entrada y aceptar solo las procedentes de una dirección IP de 1.2.3.4, modifique el XML de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="9c7d9-141">To limit inbound requests and accept only those from an IP address of 1.2.3.4 modify the XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Guardar][policies-save]

<span data-ttu-id="9c7d9-143">Cuando complete la configuración de las instrucciones de la directiva, haga clic en **Guardar** ; los cambios se propagarán inmediatamente a la puerta de enlace de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-143">When complete configuring the statements for the policy, click **Save** and the changes will be propagated to the API Management gateway immediately.</span></span>

## <span data-ttu-id="9c7d9-144"><a name="sections"> </a>Descripción de la configuración de directivas</span><span class="sxs-lookup"><span data-stu-id="9c7d9-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="9c7d9-145">Una directiva es una serie de declaraciones que se ejecutan en orden para una solicitud y una respuesta.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="9c7d9-146">La configuración se divide adecuadamente en las secciones `inbound`, `backend`, `outbound` y `on-error`, como se muestra en la siguiente configuración.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-146">The configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements to be applied to the request go here -->
  </inbound>
  <backend>
    <!-- statements to be applied before the request is forwarded to 
         the backend service go here -->
  </backend>
  <outbound>
    <!-- statements to be applied to the response go here -->
  </outbound>
  <on-error>
    <!-- statements to be applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="9c7d9-147">Si se produce un error durante el procesamiento de una solicitud, los pasos restantes de las secciones `inbound`, `backend` o `outbound` se omiten y la ejecución salta a las instrucciones de la sección `on-error`.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-147">If there is an error during the processing of a request, any remaining steps in the `inbound`, `backend`, or `outbound` sections are skipped and execution jumps to the statements in the `on-error` section.</span></span> <span data-ttu-id="9c7d9-148">Mediante la colocación de instrucciones de directiva en la sección `on-error` puede revisar el error con la propiedad `context.LastError`, inspeccionar y personalizar la respuesta de error con la directiva `set-body` y configurar lo que ocurre si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-148">By placing policy statements in the `on-error` section you can review the error by using the `context.LastError` property, inspect and customize the error response using the `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="9c7d9-149">Existen códigos de error para pasos integrados y errores que pueden producirse durante el procesamiento de las instrucciones de directiva.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-149">There are error codes for built-in steps and for errors that may occur during the processing of policy statements.</span></span> <span data-ttu-id="9c7d9-150">Para más información, consulte [Control de errores en las directivas de administración de API](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c7d9-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="9c7d9-151">Como las directivas se pueden especificar en distintos niveles (global, de producto, de API y de operación), la configuración ofrece una manera de que se especifique el orden en el que se ejecutan las instrucciones de la definición de la directiva con respecto a la directiva principal.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-151">Since policies can be specified at different levels (global, product, api and operation) the configuration provides a way for you to specify the order in which the policy definition's statements execute with respect to the parent policy.</span></span> 

<span data-ttu-id="9c7d9-152">Los ámbitos de la directiva se evalúan en el orden siguiente.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-152">Policy scopes are evaluated in the following order.</span></span>

1. <span data-ttu-id="9c7d9-153">Ámbito global</span><span class="sxs-lookup"><span data-stu-id="9c7d9-153">Global scope</span></span>
2. <span data-ttu-id="9c7d9-154">Ámbito del producto</span><span class="sxs-lookup"><span data-stu-id="9c7d9-154">Product scope</span></span>
3. <span data-ttu-id="9c7d9-155">Ámbito de la API</span><span class="sxs-lookup"><span data-stu-id="9c7d9-155">API scope</span></span>
4. <span data-ttu-id="9c7d9-156">Ámbito de la operación</span><span class="sxs-lookup"><span data-stu-id="9c7d9-156">Operation scope</span></span>

<span data-ttu-id="9c7d9-157">Las instrucciones dentro de ellos se evalúan según la ubicación del elemento `base` , si existe.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-157">The statements within them are evaluated according to the placement of the `base` element, if it is present.</span></span> <span data-ttu-id="9c7d9-158">Una directiva global no tiene una directiva principal y el uso del elemento `<base>` en ella no surte efecto.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-158">Global policy has no parent policy and using the `<base>` element in it has no effect.</span></span>

<span data-ttu-id="9c7d9-159">Por ejemplo, si tiene una directiva de nivel global y una directiva configurada para una API, cuando se use esa directiva en concreto, se aplicarán ambas directivas.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-159">For example, if you have a policy at the global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="9c7d9-160">Administración de API tiene en cuenta el orden determinista de declaraciones de directiva combinadas mediante el elemento base.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-160">API Management allows for deterministic ordering of combined policy statements via the base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="9c7d9-161">En la definición de directiva del ejemplo anterior, la instrucción `cross-domain` se ejecutaría antes de las directivas superiores que, a su vez, irían seguidas de la directiva `find-and-replace`.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-161">In the example policy definition above, the `cross-domain` statement would execute before any higher policies which would in turn, be followed by the `find-and-replace` policy.</span></span> 

<span data-ttu-id="9c7d9-162">Para ver las directivas en el ámbito actual en el editor de directivas, haga clic en **Recalcular la directiva en vigor del ámbito seleccionado**.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-162">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c7d9-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c7d9-163">Next steps</span></span>
<span data-ttu-id="9c7d9-164">Visualice el siguiente vídeo acerca de expresiones de directivas.</span><span class="sxs-lookup"><span data-stu-id="9c7d9-164">Check out following video on policy expressions.</span></span>

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
