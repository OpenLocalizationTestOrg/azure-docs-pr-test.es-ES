---
title: "Modelo de datos de telemetría de Azure Application Insights: contexto de telemetría | Microsoft Docs"
description: "Modelo de datos de contexto de telemetría de Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: d6a0cad8bda6ca68aa691867e84f540c5ac9f6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="cf4a6-103">Contexto de telemetría: modelo de datos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="cf4a6-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="cf4a6-104">Cada elemento de telemetría puede tener campos de contexto fuertemente tipados.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="cf4a6-105">Cada campo permite un escenario de supervisión específico.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="cf4a6-106">Use la recopilación de propiedades personalizadas para guardar información contextual personalizada o específica de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-106">Use the custom properties collection to store custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="cf4a6-107">Versión de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cf4a6-107">Application version</span></span>

<span data-ttu-id="cf4a6-108">La información de los campos de contexto de la aplicación siempre trata sobre la aplicación que envía la telemetría.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-108">Information in the application context fields is always about the application that is sending the telemetry.</span></span> <span data-ttu-id="cf4a6-109">La versión de la aplicación se usa para analizar cambios de tendencia en el comportamiento de la aplicación y su correlación con las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-109">Application version is used to analyze trend changes in the application behavior and its correlation to the deployments.</span></span>

<span data-ttu-id="cf4a6-110">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="cf4a6-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="cf4a6-111">Dirección IP de cliente</span><span class="sxs-lookup"><span data-stu-id="cf4a6-111">Client IP address</span></span>

<span data-ttu-id="cf4a6-112">La dirección IP del dispositivo cliente.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-112">The IP address of the client device.</span></span> <span data-ttu-id="cf4a6-113">Se admiten IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="cf4a6-114">Al enviar telemetría desde un servicio, el contexto de la ubicación trata sobre el usuario que inició la operación en el servicio.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-114">When telemetry is sent from a service, the location context is about the user that initiated the operation in the service.</span></span> <span data-ttu-id="cf4a6-115">Application Insights extrae la información de geolocalización de la IP del cliente y seguidamente la trunca.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-115">Application Insights extract the geo-location information from the client IP and then truncate it.</span></span> <span data-ttu-id="cf4a6-116">La IP del cliente no puede usarse por sí misma a modo de información de identificación del usuario final.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="cf4a6-117">Longitud máxima: 46</span><span class="sxs-lookup"><span data-stu-id="cf4a6-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="cf4a6-118">Tipo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="cf4a6-118">Device type</span></span>

<span data-ttu-id="cf4a6-119">Originalmente, este campo se usaba para indicar el tipo de dispositivo que usaba el usuario final de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-119">Originally this field was used to indicate the type of the device the end user of the application is using.</span></span> <span data-ttu-id="cf4a6-120">Hoy se usa principalmente para distinguir la telemetría de JavaScript con el tipo de dispositivo "Navegador" de la telemetría del lado del servidor con el tipo de dispositivo "PC".</span><span class="sxs-lookup"><span data-stu-id="cf4a6-120">Today used primarily to distinguish JavaScript telemetry with the device type 'Browser' from server-side telemetry with the device type 'PC'.</span></span>

<span data-ttu-id="cf4a6-121">Longitud máxima: 64</span><span class="sxs-lookup"><span data-stu-id="cf4a6-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="cf4a6-122">Identificador de operación</span><span class="sxs-lookup"><span data-stu-id="cf4a6-122">Operation id</span></span>

<span data-ttu-id="cf4a6-123">Es un identificador único de la operación de raíz.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-123">A unique identifier of the root operation.</span></span> <span data-ttu-id="cf4a6-124">Este identificador permite agrupar telemetría de varios componentes.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-124">This identifier allows to group telemetry across multiple components.</span></span> <span data-ttu-id="cf4a6-125">Consulte [Correlación de telemetría](application-insights-correlation.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="cf4a6-126">El identificador de la operación se crea, bien mediante una solicitud, bien mediante una vista de página.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-126">The operation id is created by either a request or a page view.</span></span> <span data-ttu-id="cf4a6-127">El resto de telemetría establece este campo en el valor de la solicitud o la vista de página que la contienen.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-127">All other telemetry sets this field to the value for the containing request or page view.</span></span> 

<span data-ttu-id="cf4a6-128">Longitud máxima: 128</span><span class="sxs-lookup"><span data-stu-id="cf4a6-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="cf4a6-129">Identificador de la operación principal</span><span class="sxs-lookup"><span data-stu-id="cf4a6-129">Parent operation ID</span></span>

<span data-ttu-id="cf4a6-130">Es el identificador único del primario inmediato del elemento de telemetría.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-130">The unique identifier of the telemetry item's immediate parent.</span></span> <span data-ttu-id="cf4a6-131">Consulte [Correlación de telemetría](application-insights-correlation.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="cf4a6-132">Longitud máxima: 128</span><span class="sxs-lookup"><span data-stu-id="cf4a6-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="cf4a6-133">Nombre de la operación</span><span class="sxs-lookup"><span data-stu-id="cf4a6-133">Operation name</span></span>

<span data-ttu-id="cf4a6-134">Este es el nombre (grupo) de la operación.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-134">The name (group) of the operation.</span></span> <span data-ttu-id="cf4a6-135">El nombre de la operación se crea, bien mediante una solicitud, bien mediante una vista de página.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-135">The operation name is created by either a request or a page view.</span></span> <span data-ttu-id="cf4a6-136">El resto de los elementos de telemetría establece este campo en el valor de la solicitud o la vista de página que la contienen.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-136">All other telemetry items set this field to the value for the containing request or page view.</span></span> <span data-ttu-id="cf4a6-137">El nombre de la operación se usa para localizar todos los elementos de telemetría de un grupo de operaciones (por ejemplo, "GET Home/Index").</span><span class="sxs-lookup"><span data-stu-id="cf4a6-137">Operation name is used for finding all the telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="cf4a6-138">Esta propiedad del contexto se usa para contestar a preguntas como "¿cuáles son las excepciones habituales que se producen en esta página?".</span><span class="sxs-lookup"><span data-stu-id="cf4a6-138">This context property is used to answer questions like "what are the typical exceptions thrown on this page."</span></span>

<span data-ttu-id="cf4a6-139">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="cf4a6-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-the-operation"></a><span data-ttu-id="cf4a6-140">Origen sintético de la operación</span><span class="sxs-lookup"><span data-stu-id="cf4a6-140">Synthetic source of the operation</span></span>

<span data-ttu-id="cf4a6-141">Nombre del origen sintético.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-141">Name of synthetic source.</span></span> <span data-ttu-id="cf4a6-142">Cierta telemetría de la aplicación puede representar tráfico sintético.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-142">Some telemetry from the application may represent synthetic traffic.</span></span> <span data-ttu-id="cf4a6-143">Puede tratarse de un robot de búsqueda que esté indexando el sitio web, de pruebas de disponibilidad del sitio o de seguimientos de bibliotecas de diagnóstico, como el propio SDK de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-143">It may be web crawler indexing the web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="cf4a6-144">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="cf4a6-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="cf4a6-145">Identificador de la sesión</span><span class="sxs-lookup"><span data-stu-id="cf4a6-145">Session id</span></span>

<span data-ttu-id="cf4a6-146">Identificador de la sesión: la instancia de la interacción del usuario con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-146">Session ID - the instance of the user's interaction with the app.</span></span> <span data-ttu-id="cf4a6-147">La información de los campos de contexto de la sesión siempre trata sobre el usuario final.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-147">Information in the session context fields is always about the end user.</span></span> <span data-ttu-id="cf4a6-148">Al enviar telemetría desde un servicio, el contexto de la sesión trata sobre el usuario que inició la operación en el servicio.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-148">When telemetry is sent from a service, the session context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="cf4a6-149">Longitud máxima: 64</span><span class="sxs-lookup"><span data-stu-id="cf4a6-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="cf4a6-150">Identificador del usuario anónimo</span><span class="sxs-lookup"><span data-stu-id="cf4a6-150">Anonymous user id</span></span>

<span data-ttu-id="cf4a6-151">Este es el identificador del usuario anónimo.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-151">Anonymous user id.</span></span> <span data-ttu-id="cf4a6-152">Representa al usuario final de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-152">Represents the end user of the application.</span></span> <span data-ttu-id="cf4a6-153">Al enviar telemetría desde un servicio, el contexto del usuario trata sobre el usuario que inició la operación en el servicio.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-153">When telemetry is sent from a service, the user context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="cf4a6-154">El [muestreo](app-insights-sampling.md) es una de las técnicas mediante las cuales se reduce al mínimo la cantidad de telemetría recopilada.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-154">[Sampling](app-insights-sampling.md) is one of the techniques to minimize the amount of collected telemetry.</span></span> <span data-ttu-id="cf4a6-155">El algoritmo de muestreo intenta muestrear toda la telemetría correlacionada para aceptarla o rechazarla.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-155">Sampling algorithm attempts to either sample in or out all the correlated telemetry.</span></span> <span data-ttu-id="cf4a6-156">El identificador del usuario anónimo se usa para muestrear la generación de puntuaciones.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-156">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="cf4a6-157">Por ello, el identificador del usuario anónimo debería ser un valor suficiente aleatorio.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-157">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="cf4a6-158">Usar el identificador del usuario anónimo para almacenar el nombre de usuario es usar el campo de forma incorrecta.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-158">Using anonymous user id to store user name is a misuse of the field.</span></span> <span data-ttu-id="cf4a6-159">Use el identificador del usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-159">Use Authenticated user id.</span></span>

<span data-ttu-id="cf4a6-160">Longitud máxima: 128</span><span class="sxs-lookup"><span data-stu-id="cf4a6-160">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="cf4a6-161">Identificador del usuario autenticado</span><span class="sxs-lookup"><span data-stu-id="cf4a6-161">Authenticated user id</span></span>

<span data-ttu-id="cf4a6-162">Este es el identificador del usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-162">Authenticated user id.</span></span> <span data-ttu-id="cf4a6-163">Este campo, el contrario al del identificador del usuario anónimo, representa al usuario con un nombre sencillo.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-163">The opposite of anonymous user id, this field represents the user with a friendly name.</span></span> <span data-ttu-id="cf4a6-164">Puesto que se trata de información de identificación personal, la mayoría de SDK no la recopilan de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-164">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="cf4a6-165">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="cf4a6-165">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="cf4a6-166">Identificador de la cuenta</span><span class="sxs-lookup"><span data-stu-id="cf4a6-166">Account id</span></span>

<span data-ttu-id="cf4a6-167">En aplicaciones multiinquilino, este es el identificador o el nombre de la cuenta con el que actúa el usuario.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-167">In multi-tenant applications this is the account ID or name, which the user is acting with.</span></span> <span data-ttu-id="cf4a6-168">Algunos ejemplos son el identificador de la suscripción de Azure Portal o el nombre del blog de la plataforma de creación de blogs.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-168">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="cf4a6-169">Longitud máxima: 1024</span><span class="sxs-lookup"><span data-stu-id="cf4a6-169">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="cf4a6-170">Rol en la nube</span><span class="sxs-lookup"><span data-stu-id="cf4a6-170">Cloud role</span></span>

<span data-ttu-id="cf4a6-171">Este es el nombre del que la aplicación forma parte.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-171">Name of the role the application is a part of.</span></span> <span data-ttu-id="cf4a6-172">Se asigna directamente al nombre del rol de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-172">Maps directly to the role name in azure.</span></span> <span data-ttu-id="cf4a6-173">También puede usarse para distinguir microservicios que formen parte de una única aplicación.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-173">Can also be used to distinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="cf4a6-174">Longitud máxima: 256</span><span class="sxs-lookup"><span data-stu-id="cf4a6-174">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="cf4a6-175">Instancia de rol en la nube</span><span class="sxs-lookup"><span data-stu-id="cf4a6-175">Cloud role instance</span></span>

<span data-ttu-id="cf4a6-176">Este es el nombre de la instancia en la que se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-176">Name of the instance where the application is running.</span></span> <span data-ttu-id="cf4a6-177">El nombre de equipo del nombre de instancia local para Azure.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-177">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="cf4a6-178">Longitud máxima: 256</span><span class="sxs-lookup"><span data-stu-id="cf4a6-178">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="cf4a6-179">Interno: versión del SDK</span><span class="sxs-lookup"><span data-stu-id="cf4a6-179">Internal: SDK version</span></span>

<span data-ttu-id="cf4a6-180">Esta es la versión del SDK.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-180">SDK version.</span></span> <span data-ttu-id="cf4a6-181">Consulte https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification para obtener información.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-181">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="cf4a6-182">Longitud máxima: 64</span><span class="sxs-lookup"><span data-stu-id="cf4a6-182">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="cf4a6-183">Interno: nombre del nodo</span><span class="sxs-lookup"><span data-stu-id="cf4a6-183">Internal: Node name</span></span>

<span data-ttu-id="cf4a6-184">Este campo representa el nombre del nodo que se usa para la facturación.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-184">This field represents the node name used for billing purposes.</span></span> <span data-ttu-id="cf4a6-185">Úselo para invalidar la detección estándar de nodos.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-185">Use it to override the standard detection of nodes.</span></span>

<span data-ttu-id="cf4a6-186">Longitud máxima: 256</span><span class="sxs-lookup"><span data-stu-id="cf4a6-186">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="cf4a6-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf4a6-187">Next steps</span></span>

- <span data-ttu-id="cf4a6-188">Obtenga información sobre cómo [ampliar y filtrar la telemetría](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="cf4a6-188">Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="cf4a6-189">Consulte [modelo de datos](application-insights-data-model.md) para los tipos y el modelo de datos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-189">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="cf4a6-190">Compruebe la [configuración](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) de la recopilación de propiedades estándar de contexto.</span><span class="sxs-lookup"><span data-stu-id="cf4a6-190">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
